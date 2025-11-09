The code `if (!meal) { notFound(); }` is used in **Next.js** to handle cases where a requested resource does not exist.

### **🛠 Explanation:**

- `notFound()` is a built-in Next.js function that triggers the **`not-found.tsx`** page when a requested item is not found.
- `meal` is likely fetched using a **slug** or **ID** from a database or file system.
- If `meal` is `undefined` or `null`, it means the requested meal doesn't exist, so we trigger `notFound()` to show a **custom 404 page**.

---

### **✅ Example: Using `notFound()` in a Dynamic Route**

```tsx
import { notFound } from "next/navigation";
import { getMeal } from "@/lib/meals";

export default async function Page({ params }: { params: { slug: string } }) {
  const meal = await getMeal(params.slug);

  if (!meal) {
    notFound(); // Redirects to the 404 "not-found.tsx" page
  }

  return (
    <div>
      <h1>{meal.title}</h1>
      <p>{meal.description}</p>
    </div>
  );
}
```


---

### **📌 When to Use `notFound()`?**

- When fetching data from a **database, API, or file system**, and the resource **doesn’t exist**.
- In **dynamic routes (`app/[slug]/page.tsx`)**, to handle invalid slugs.
- To ensure users don’t see an empty page or error when accessing a **nonexistent resource**.

---

### **🛠 Customizing the Not Found Page**

You can create a custom `not-found.tsx` in your route directory:

#### **📌 `/app/not-found.tsx` (Global 404 Page)**

```tsx
export default function NotFoundPage() {
  return (
    <div>
      <h1>404 - Page Not Found</h1>
      <p>Sorry, we couldn't find what you were looking for.</p>
    </div>
  );
}
```

#### **📌 `/app/meals/not-found.tsx` (Scoped 404 for Meals)**

```tsx
export default function NotFoundMeal() {
  return (
    <div>
      <h1>Meal Not Found</h1>
      <p>Sorry, the requested meal does not exist.</p>
    </div>
  );
}
```


This makes sure users see a **contextual 404 page** depending on where they are.

---

### **🚀 Summary**

✔ `notFound()` redirects to the **404 page** when a resource is missing.  
✔ Best for handling **invalid slugs** in **dynamic routes**.  
✔ You can **customize 404 pages** globally or per route.