### **🛠 When Does `params` Become a Promise?**

- If your component is **async** in a `page.tsx` file (inside the `app` directory), `params` will be **a Promise**.
- This means you **must `await` it** before accessing its values.

### **✅ Example (Next.js 15)**

```tsx
export default   function Page({
  params,
}: {
  params: Promise<{ slug: string }>;
}) {
  const { slug } = await params; // ✅ params is a Promise, so we must await it.
  return <h1>Post: {slug}</h1>;
}
```

### **⚡ Why Did This Change?**

1. **Better async handling**: Since `params` is often fetched dynamically, making it a Promise aligns it with other async data sources.
2. **Consistent API**: Now, everything async in Next.js behaves in a uniform way (e.g., fetching data and using params follow the same pattern).
3. **Future-proofing**: Although Next.js 15 allows accessing `params` synchronously (for backward compatibility), this behavior **will be deprecated in future versions**.

---

### **🔍 What If You Don’t Want `params` as a Promise?**

You can **access it synchronously**, but this behavior **will not last forever**:

```tsx
export default async function Page({ params }: { params: { slug: string } }) {
  return <h1>Post: {params.slug}</h1>; // 🚨 Works for now, but will be deprecated
}
```

---

### **📝 Summary**

- In **Next.js 15**, `params` is a **Promise** inside an `async` Server Component.
- You **must `await` it** before accessing its properties.
- The old synchronous behavior is **still supported** but will be **removed in future versions**.

### **✅ Correct Way to Handle `params` in Next.js 15**

Since `params` is now a **Promise**, you **must** `await` it inside an `async` function.

```tsx
export default async function Page({
  params,
}: {
  params: Promise<{ slug: string }>;
}) {
  const { slug } = await params; // ✅ Must await params
  return <h1>My Post: {slug}</h1>;
}
```

---

### **📌 Explanation**

- In **Next.js 14 and earlier**, `params` was synchronous:
    
    `const { slug } = params; // No need to await`
    
- In **Next.js 15**, `params` is now a **Promise**, so you must `await` it:
    
    `const { slug } = await params; // ✅ Required in Next.js 15`
    
- This change helps **unify async behavior** in Next.js, but **synchronous access is still supported for now** for backward compatibility. **However, this will be deprecated soon.**

---

### **🚀 How to Future-Proof Your Code?**

If you want **future-proof code**, **always `await` params`** in an async component.