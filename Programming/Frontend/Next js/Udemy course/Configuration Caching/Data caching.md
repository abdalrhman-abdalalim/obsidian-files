 ## 📦 Next.js — Data Caching & Revalidation

### 🧠 Core Idea

Next.js **caches and reuses fetched data** during rendering (SSR/ISR/SSG), until it is time to **revalidate** the data.

---

## 🔁 `fetch()` Request Caching Configuration

### ✅ You can control caching behavior with:

```tsx
fetch("https://api.example.com/data", {
  cache: "force-cache" | "no-store",
  next: {
    revalidate: number // in seconds
  }
});
```

### 🔹 `cache` Options:

|Option|Description|Default in|
|---|---|---|
|`"force-cache"`|Always uses cache, even between builds|Next 13/14|
|`"no-store"`|Disables caching entirely|Next 15|

### 🔹 `next.revalidate`:

- Tells Next **how many seconds** to keep using the cached data before re-fetching.
    
- Example:
    
	`fetch(url, {   next: { revalidate: 10 } });`
	
- This means: **reuse cached data for 10 seconds**, then re-fetch.
    

---

## ⚙️ Page-Level Cache Control

You can also control caching at the **page or component level** with exports:

```tsx
// Route segment config
export const revalidate = 5; // revalidate every 5 seconds

// Fully dynamic, disable caching
export const dynamic = 'force-dynamic'; // same as "no-store"

// Fully static, enable full cache
export const dynamic = 'force-static';  // same as "force-cache"
```


---

## 🧪 Forcing No Cache in Component Code

```tsx
import { unstable_noStore } from 'next/cache';

export default function Page() {
  unstable_noStore(); // disables caching inside this component
  // do your fetch logic here
}
```

Use this when you need **true dynamic behavior**, e.g., dashboards, admin panels, etc.

---

## 🔍 Summary Table

|Control Point|Usage|
|---|---|
|`cache` in `fetch()`|`"force-cache"` or `"no-store"`|
|`next.revalidate`|Reuse duration in seconds|
|`export const revalidate`|Page-level revalidate override|
|`export const dynamic`|Force dynamic/static behavior|
|`unstable_noStore()`|Disable cache **inside component**|

---

## 💡 Real-World Example

```tsx
// Example with revalidation every 30 seconds
export const revalidate = 30;

export default async function Page() {
  const res = await fetch("https://api.example.com/data", {
    next: { revalidate: 30 }
  });

  const data = await res.json();
  return <pre>{JSON.stringify(data, null, 2)}</pre>;
}
```
