### **🔹 Next.js and Aggressive Caching**

- Next.js **caches everything aggressively** to improve performance.
- Static pages and **data fetching results** (e.g., `fetch()`) are cached automatically.
- You can control caching behavior using:
    - `revalidate` (ISR - Incremental Static Regeneration)
    - `fetch` options (`cache: 'no-store'` for dynamic data)

---

### **🔹 `loading.tsx` (Per Layout & Page-Level Loading)**

- The `loading.tsx` file is **specific to a layout** and applies to: ✅ **All sibling pages**  
    ✅ **All nested pages**  
    ✅ **Layouts (affects all children inside the layout)**
- You can add a **`loading.tsx`** to **any page or layout**, and it will automatically show during navigation.

#### **Example:**

📂 `app/dashboard/loading.tsx`

`export default function Loading() {   return <p>Loading...</p>; }`

🚀 Now, every page inside `/dashboard/` will show this loading UI when transitioning!

---

### **🔹 Suspense in React (For Selective Loading)**

- **Suspense** prevents **loading the whole page at once**.
- Instead of blocking the entire page, it **renders a fallback UI** while loading specific parts.

#### **Example:**

```tsx
import { Suspense } from "react";
import HeavyComponent from "./HeavyComponent";

export default function Page() {
  return (
    <Suspense fallback={<p>Loading component...</p>}>
      <HeavyComponent />
    </Suspense>
  );
}
```

🔥 **Why use Suspense?**

- Improves **user experience** by showing partial content.
- Helps with **lazy loading** expensive components.

---

### **🔹 Error Handling with `error.tsx`**

- `error.tsx` is used to handle **client-side errors**.
- It must be placed inside a layout or page.

#### **Example:**

📂 `app/dashboard/error.tsx`

```tsx
"use client"; // Required for error.tsx

export default function ErrorPage({ error }: { error: Error }) {
  return (
    <div>
      <h2>Something went wrong!</h2>
      <p>{error.message}</p>
    </div>
  );
}
```


✅ **When is `error.tsx` triggered?**

- If a component inside the layout **throws an error**.

---

### **🔹 `not-found.tsx` (Handling 404s)**

- Used when a **route does not exist**.
- It **automatically renders** when a page returns `notFound()`.

#### **Example:**

📂 `app/not-found.tsx`

`export default function NotFoundPage() {   return <h1>404 - Page Not Found</h1>; }`

✅ **Triggers automatically** if:

```tsx
import { notFound } from "next/navigation";

export default function Page() {
  const data = null;
  if (!data) notFound(); // Redirects to `not-found.tsx`
  return <p>Page content</p>;
}

```

---

### **🔥 Summary**

✅ **Next.js caches aggressively** for better performance.  
✅ **`loading.tsx`** works at the **layout and page level** (affects all children).  
✅ **Suspense** allows **lazy loading of components** instead of blocking the entire page.  
✅ **`error.tsx`** handles **client-side errors** dynamically.  
✅ **`not-found.tsx`** is used to manage **invalid paths (404s)** automatically.