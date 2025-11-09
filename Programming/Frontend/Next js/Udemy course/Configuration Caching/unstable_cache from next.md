#### 📥 Import

`import { unstable_cache } from "next/cache";`

---

#### 🔧 What is `unstable_cache`?

`unstable_cache` is a utility provided by **Next.js** that lets you **cache the result of a function** on the **server**.  
It works similarly to React's `cache`, but it's **specific to Next.js** and supports **revalidation strategies**.

> Unlike `react/cache`, this function returns a **Promise** and supports **tag-based revalidation**.

---

#### 📦 Function Signature

`unstable_cache(fn, keyParts, options)`

- `fn`: The asynchronous function whose result you want to cache.
    
- `keyParts`: Array of keys used to uniquely identify this cache entry.
    
- `options`: Configuration object.
    

---

#### ⚙️ Options

```tsx
{
  revalidate: 5, // Number of seconds after which the cache is considered stale.
  tags: ["msg"]  // Tags used to manually invalidate cache using `revalidateTag()`.
}
```

---

#### 📌 Example Usage

```tsx
import { unstable_cache } from "next/cache";

const getMessages = unstable_cache(
  async () => {
    const res = await fetch("https://api.example.com/messages");
    return res.json();
  },
  ["messages"], // Unique cache key
  {
    revalidate: 5,
    tags: ["msg"],
  }
);
```

---

#### 🔄 Manual Revalidation

You can revalidate a tag manually like this:

```tsx
import { revalidateTag } from "next/cache";

revalidateTag("msg");
```

This will **invalidate all cached results** tagged with `"msg"` and refetch them on the next request.