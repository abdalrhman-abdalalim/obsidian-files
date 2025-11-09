## 📦 Next.js — Request Memoization & Caching

### 🧠 Concept: **Request Memoization**

Next.js **memoizes** (remembers) fetch requests made **with the same configuration** to avoid unnecessary duplicate requests during a single server-render or during SSR/ISR.

### 🔁 What Happens:

- If **two or more `fetch()` calls** are made with **identical parameters** (URL, headers, options), **Next.js automatically de-duplicates** them.
    
- It **treats them as one request** and **reuses the response**.
    

### ✅ Benefits:

- Reduces **unnecessary network calls**.
    
- Boosts **performance** during SSR or ISR.
    
- Keeps your data **consistent** across the render cycle.
    
- Saves **bandwidth and computing time**.
    

### 📌 Example:

```tsx
// Both fetches below are considered identical
const data1 = await fetch("https://api.example.com/data", {
  next: { revalidate: 60 }
});

const data2 = await fetch("https://api.example.com/data", {
  next: { revalidate: 60 }
});

// Only one actual request is sent
```
### 📁 Cache Layer:

- **Caching is scoped** to the render duration (SSR, ISR, or during a static generation).
    
- This means the memoization happens **within that request cycle**, not globally or persistently between deployments.
    
- You can use the `next.revalidate` config to **persist the cache** beyond a single request.
    

---

## 🧭 When Does This Happen?

|Scenario|Memoization Active?|Notes|
|---|---|---|
|SSR (getServerSideProps, server components)|✅ Yes|Automatic de-duplication|
|ISR (Incremental Static Regeneration)|✅ Yes|Based on `revalidate`|
|CSR (Client Side fetch)|❌ No|You'll need your own cache (e.g., SWR, React Query)|

---

## ⚙️ How to Control It

Use the `next` config in `fetch()`:


`fetch(url, {   next: {     revalidate: 10 // seconds   } });`

- This ensures caching is **enabled** for a defined period.
    
- If **two fetches** use the same `url` and `revalidate`, **Next.js will cache** and re-use the response.