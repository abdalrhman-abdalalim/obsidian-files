> **he `loading.tsx` file becomes active whenever your route is waiting for a component to fetch and render its content.**  
> Next.js automatically shows this loading UI while the data is being fetched in a Server Component or any `async` logic is still pending.

---

## 🔍 How It Works

If you have a structure like:

```tsx
app/
 └─ products/
     ├─ [id]/
     │   ├─ page.tsx     ← async Server Component
     │   └─ loading.tsx  ← shown while `page.tsx` is loading
```

Then `loading.tsx` will **automatically** show up when:

- The `page.tsx` is an `async` component (e.g. awaiting data)
    
- Or any nested layout/component is still loading
    

---

## ✅ Example

### `page.tsx`

```tsx
export default async function ProductPage({ params }) {
  const res = await fetch(`https://dummyjson.com/products/${params.id}`);
  const product = await res.json();

  return <div>{product.title}</div>;
}

```

### `loading.tsx`

`export default function Loading() {   return <div>Loading product...</div>; }`

🟢 Result: When the page is loading (i.e., the `await` hasn't finished), **Next.js shows `loading.tsx` automatically.**