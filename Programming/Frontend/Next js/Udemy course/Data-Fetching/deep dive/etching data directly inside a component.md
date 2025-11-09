> **Fetching data directly inside a component is the standard approach you should use when working with Next.js (App Router).**  
> This is especially true when using **Server Components**, which allow you to fetch data with `async`/`await` directly at the top level of your component — without needing `useEffect`, `getServerSideProps`, or `getStaticProps`.

---

## 🔍 Explanation: Why This Is the New Standard in Next.js (App Router)

In the **App Router** (introduced in Next.js 13+), the standard way to fetch data is:

```tsx
// Server Component
export default async function ProductPage() {
  const res = await fetch("https://dummyjson.com/products/1");
  const product = await res.json();

  return (
    <div>
      <h1>{product.title}</h1>
      <p>{product.description}</p>
    </div>
  );
}
```

---

### ✅ Why This Is the Preferred Way

|🧠 Reason|✅ Benefit|
|---|---|
|**Cleaner code**|No need for separate `getServerSideProps` or `getStaticProps`|
|**Better performance**|Data is fetched and rendered on the server before sending HTML|
|**SEO-friendly**|Content is included in the server-rendered HTML|
|**Works with Suspense**|You can use `Suspense` for granular loading UI|
|**Built-in caching & revalidation**|You can control freshness with `revalidate`, `cache: 'no-store'`, etc.|

---

## ⚠️ When NOT to Fetch Inside the Component

If you're building a **Client Component** (like something interactive or user-specific), fetching inside the component requires `useEffect`:

```tsx
"use client";

import { useEffect, useState } from "react";

const ClientSideComponent = () => {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch("/api/data")
      .then(res => res.json())
      .then(setData);
  }, []);

  return <div>{data ? data.name : "Loading..."}</div>;
};
```