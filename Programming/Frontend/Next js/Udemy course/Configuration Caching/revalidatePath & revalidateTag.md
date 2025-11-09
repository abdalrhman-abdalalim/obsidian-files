## 🔁 Next.js — Revalidation Methods

### 1. 🛣️ `revalidatePath(path, type?)`

**Usage:**

```tsx
import { revalidatePath } from 'next/cache';

revalidatePath('/dashboard');
// OR with type
revalidatePath('/dashboard', 'layout');
```

### 🔍 How it Works:

- **By default**, it only revalidates the **exact `page`** you provide.
    
- So nested routes (e.g., `/dashboard/settings`) **won’t be revalidated** if you only revalidate `/dashboard`.
    

### 🔄 Optional Second Argument:

|Type|Effect|
|---|---|
|`"page"`|(default) only revalidates the specific page|
|`"layout"`|revalidates the layout **and all nested pages**|

---

### 2. 🏷️ `revalidateTag(tag)`

**Powerful when you want to revalidate multiple routes together.**

### ✨ Setup

In your `fetch()` call:

```tsx
await fetch('https://api.example.com/messages', {
  next: {
    tags: ['messages']
  }
});
```


Then you can use:

`import { revalidateTag } from 'next/cache';  revalidateTag('messages');`

✅ This will revalidate **all fetches** that use the `'messages'` tag — even across multiple pages/components.

---

## ✅ Why Use Tags?

|Benefit|Description|
|---|---|
|🎯 Targeted|Revalidate **only** the parts of your app that depend on the tag|
|⚡ Efficient|Update **multiple pages** in **one line**|
|🧩 Flexible|Great for CMS, dashboard updates, notifications, etc.|