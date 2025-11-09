### 📦 `useCart` – Fetch and Cache Cart Data Using React Query

This custom hook leverages **React Query** to fetch and cache the current cart data for either **authenticated users** or **guests** (via a visitor token). It also ensures smooth UX through caching and optionally keeps previous cart data while refetching.

---

### 📁 File: `hooks/useCart.ts`

---

### ✅ Hook Purpose

`useCart` fetches cart information using either:

- Authenticated user's token (`Authorization`)
    
- Or a guest's token (`X-Visitor-Token`)
    
- If no token is available, it hits the cart endpoint to generate a new visitor token.
    

---

### 🔧 How it works

#### 1. **Token Logic**:

- `getAuthToken()`: fetches logged-in user token.
    
- `getVisitorToken()`: fetches saved guest token.
    
- If neither is present, it fetches the cart anonymously and saves the new visitor token to local Storage.
    

#### 2. **Data Fetching with React Query**:


`useQuery<Cart>({   queryKey: ["cart"],   queryFn: fetchCart,   ...options })`

- `queryKey`: identifies this data in the cache.
    
- `queryFn`: fetches cart data via Axios.
    
- `options`: supports `enabled` and `keepPreviousData`.
    

#### 3. **Caching & Re-fetching**:

- By default, React Query will **cache the cart**, **refetch on focus**, and **keep stale data** until the fetch finishes.
    

#### 4. **Fast Updates / Optimistic UI** (💡 future enhancement)

To support _fast cart updates_ (e.g., add/remove items), you can:

- Use `useMutation` for cart updates (add/remove items)
    
- Use `queryClient.setQueryData(["cart"], updaterFn)` to update cache instantly
    
- Optionally rollback if mutation fails
    

```tsx
// Example: Optimistic update for adding an item
const queryClient = useQueryClient();
const mutation = useMutation(addToCart, {
  onMutate: async (newItem) => {
    await queryClient.cancelQueries(["cart"]);
    const prevCart = queryClient.getQueryData<Cart>(["cart"]);

    queryClient.setQueryData(["cart"], (old: Cart) => {
      return {
        ...old,
        data: {
          ...old.data,
          cart: {
            ...old.data.cart,
            items: [...old.data.cart.items, newItem],
            total_quantity: old.data.cart.total_quantity + 1,
          },
        },
      };
    });

    return { prevCart };
  },
  onError: (_, __, context) => {
    queryClient.setQueryData(["cart"], context.prevCart);
  },
  onSettled: () => {
    queryClient.invalidateQueries(["cart"]);
  },
});

```

---

### ⚙️ Customizable Options:

|Option|Type|Description|
|---|---|---|
|`enabled`|boolean|Whether to enable the query initially|
|`keepPreviousData`|boolean|Keeps old data while refetching|

---

### 🧠 Best Practices

- Always provide `visitor_token` for guest users to persist cart data
    
- Use `queryKey` consistently to avoid cache mismatches
    
- Use `queryClient.setQueryData` to update UI instantly (Optimistic Updates)
    
- Combine with `useMutation` for modifying cart (add/remove/update items)

## 🚀 ما هي `onMutate`؟

`onMutate` هي **callback function** في `useMutation` بتتسمى **قبل** ما تبدأ الـ mutation نفسها.

> ✨ الهدف الرئيسي منها:  
> عمل **Optimistic Update** — يعني تحديث البيانات في الـ UI فورًا _قبل_ ما السيرفر يرد، عشان تحس المستخدم إن كل حاجة سريعة.


## 🔄 إيه اللي بيحصل بالترتيب؟

1. **قبل** ما `mutationFn` يتنفذ، `onMutate` بتشتغل.
    
2. React Query بتوقف أي query بتسحب نفس البيانات (`["cart"]`).
    
3. بتاخد نسخة من البيانات القديمة.
    
4. بتعمل تحديث للكاش على طول (بدون انتظار API).
    
5. لو حصل Error، بنرجّع الكاش زي ما كان.
    
6. بعد كده في `onSettled`, نرجّع نطلب الداتا من الـ backend (refetch).

## 🧠 ملاحظات مهمة:

- `onMutate` دايمًا بيرجع قيمة (غالبًا object فيها `context`) تستخدمها في `onError`.
    
- لازم تستخدمها لما عايز _تحسّن تجربة المستخدم_ وتقلل وقت الانتظار.
    
- من غير `onMutate`، المستخدم هيستنى API تخلص عشان يشوف التحديث = بطء.