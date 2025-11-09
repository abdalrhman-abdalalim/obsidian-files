## ✅ **How `generateMetadata()` Works**

- This function **runs on the server** before rendering the page.
- It **fetches dynamic data** and returns metadata for the page.
- Useful for **dynamic title, description, and Open Graph metadata** (e.g., for products, blogs, or user profiles).

---

## 🔥 **Example: Dynamic Metadata for a Product Page**

```tsx
import { Metadata } from "next";

// Function to fetch product data (dummy API example)
async function getProduct(id: string) {
  const res = await fetch(`https://dummyjson.com/products/${id}`);
  return res.json();
}

// Generate dynamic metadata
export async function generateMetadata({ params }: { params: { id: string } }): Promise<Metadata> {
  const product = await getProduct(params.id);

  return {
    title: product.title,
    description: product.description,
    openGraph: {
      title: product.title,
      description: product.description,
      images: [product.thumbnail],
    },
  };
}

// Page Component
export default async function ProductPage({ params }: { params: { id: string } }) {
  const product = await getProduct(params.id);

  return (
    <div>
      <h1>{product.title}</h1>
      <p>{product.description}</p>
      <img src={product.thumbnail} alt={product.title} />
    </div>
  );
}

```

---

## 🏆 **Key Takeaways**

✅ **Metadata updates dynamically per page request**  
✅ **Runs on the server for better performance**  
✅ **Supports Open Graph for social sharing**  
✅ **Works with `fetch()` to get dynamic data**

Would you like help implementing this in your project? 🚀

4o