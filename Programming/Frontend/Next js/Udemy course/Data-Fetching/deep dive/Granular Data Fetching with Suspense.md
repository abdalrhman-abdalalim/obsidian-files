## 🎯 What is Granular Data Fetching with Suspense?

> **Granular data fetching** means loading **specific parts of a page independently**, so each section can:

- Fetch its own data
    
- Show its own loading UI
    
- Render as soon as its data is ready — without waiting for the entire page
    

This is powered by **React Suspense** + **Server Components** in the Next.js **App Router**.

---

## ✅ Why It’s Awesome

|Feature|Benefit|
|---|---|
|Independent loading states|Better UX — sections load as they’re ready|
|Fine-tuned control|Only show loaders for the parts that need them|
|Performance boost|Reduce time to first render|
|Server-side by default|SEO-friendly + faster hydration|

---

## 🧪 Real Example

Imagine you're building a product page with:

- **Product Info**
    
- **Customer Reviews**
    
- **Recommended Products**
    

You want each to load independently.

---

### 📁 File Structure

```tsx
app/
 └─ product/
     └─ [id]/
         ├─ page.tsx
         ├─ ProductInfo.tsx
         ├─ Reviews.tsx
         └─ Recommendations.tsx
```

---

### 🔧 `page.tsx`

```tsx
import { Suspense } from "react";
import ProductInfo from "./ProductInfo";
import Reviews from "./Reviews";
import Recommendations from "./Recommendations";

export default function ProductPage({ params }: { params: { id: string } }) {
  return (
    <div>
      <Suspense fallback={<p>Loading product info...</p>}>
        <ProductInfo id={params.id} />
      </Suspense>

      <Suspense fallback={<p>Loading reviews...</p>}>
        <Reviews id={params.id} />
      </Suspense>

      <Suspense fallback={<p>Loading recommendations...</p>}>
        <Recommendations id={params.id} />
      </Suspense>
    </div>
  );
}
```


---

### 🔧 `ProductInfo.tsx` (Server Component)

```tsx
const ProductInfo = async ({ id }: { id: string }) => {
  const res = await fetch(`https://dummyjson.com/products/${id}`);
  const product = await res.json();

  return <h1>{product.title}</h1>;
};

export default ProductInfo;
```

``const ProductInfo = async ({ id }: { id: string }) => {   const res = await fetch(`https://dummyjson.com/products/${id}`);   const product = await res.json();    return <h1>{product.title}</h1>; };  export default ProductInfo;``

Do the same for `Reviews` and `Recommendations` — each fetches independently!