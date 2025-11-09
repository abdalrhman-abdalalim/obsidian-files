Group routing in Next.js (e.g., folders like `(admin)`, `(shop)`, `(marketing)`) is a powerful feature to help you **organize layouts without affecting the URL path**.

These folders are **ignored in the URL**, meaning the folder name doesn’t appear in the route path, but they help structure and manage different layouts.

---

### 🧭 Handling the Root Route `/`

If you're using **multiple group routes** and you want to define the main landing page (`/`), then:

> ✅ **You must place a `page.tsx` in one of the group folders** to handle the `/` route.

For example:

```css
app/
├─ (main)/
│  ├─ layout.tsx
│  ├─ page.tsx ← Handles "/"
├─ (dashboard)/
│  ├─ layout.tsx
│  ├─ stats/
│  │  ├─ page.tsx ← Handles "/stats"
```

- Even though both `(main)` and `(dashboard)` are ignored in the path,
    
- The `page.tsx` inside `(main)` serves `/` because it's the **first match in the route tree** that contains a `page.tsx` at root level.
    

---

### 🚫 What happens if you don’t define it?

If you structure your app using only group routes and **forget to include a `page.tsx`** in **any of them at the top level**, then navigating to `/` will result in a **404** — because Next.js doesn’t know what to render at the root.

---

### ✅ Best Practice

Always make sure that **at least one of your group folders contains a `page.tsx` file** to serve the homepage (or root layout level).