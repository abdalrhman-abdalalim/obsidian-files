## 📌 **`usePathname()` in Next.js**

`usePathname()` is a hook provided by **Next.js** (App Router) to get the **current URL pathname** in your application.

### ✅ **How to Use `usePathname()`**

First, import the hook from `next/navigation`:

tsx

CopyEdit

`"use client"; // This is a Client Component  import { usePathname } from "next/navigation";  export default function PathDisplay() {   const path = usePathname(); // Get the current URL path    return <p>Current Path: {path}</p>; }`

---

## 🔍 **Example Scenarios**

Since `usePathname()` returns a string, you can apply **any JavaScript string methods** on it.

### **1️⃣ Check if the User is on a Specific Page**

`const path = usePathname();  if (path === "/dashboard") {   console.log("User is on the dashboard"); }`

### **2️⃣ Extract a Dynamic Segment**

Let's say you have a dynamic route like `/products/123`, and you need to extract `123`:


`const path = usePathname(); const productId = path.split("/").pop(); // Extracts the last part of the URL console.log(productId); // Output: "123"`

### **3️⃣ Highlight Active Links**

Useful for styling the active link in a navigation menu:

```tsx
import Link from "next/link";
import { usePathname } from "next/navigation";

export default function Navbar() {
  const path = usePathname();

  return (
    <nav>
      <Link href="/" className={path === "/" ? "active" : ""}>Home</Link>
      <Link href="/about" className={path === "/about" ? "active" : ""}>About</Link>
    </nav>
  );
}
```

```css
.active {
  font-weight: bold;
  color: blue;
}
```

### **4️⃣ Check If Path Includes a Keyword**

`const path = usePathname();  if (path.includes("admin")) {   console.log("User is in the admin panel"); }`

---

## ⚠️ **Important Notes**

1. **Client Component Only**
    
    - `usePathname()` only works in **Client Components** because it's part of `next/navigation`.
    - You **must** add `"use client"` at the top of your file.
2. **Does Not Include Query Parameters**
    
    - `usePathname()` **only returns the pathname**, not query strings (`?key=value`).
    - If you need query parameters, use `useSearchParams()` instead.
3. **Does Not Include Hashes (`#`)**
    
    - If you need to track hash changes (`/page#section`), use `window.location.hash` inside `useEffect`.

---

## 🚀 **Final Thoughts**

- **`usePathname()` gets the current URL path** (e.g., `/dashboard`, `/products/123`).
- **You can use all string methods** on it to manipulate or extract parts of the path.
- **Useful for checking routes, styling active links, and extracting dynamic segments**.
- **It must be used in Client Components**.

Let me know if you need more examples! 😃🚀
