In **Next.js App Router**, the `layout.tsx` file is used to define a shared layout for a group of pages.

### **🛠 How It Works**

1. **`metadata`** → Adds SEO metadata (title, description, OpenGraph tags, etc.).
2. **`RootLayout` Component**:
    - Wraps all pages in the `app/` directory.
    - Contains a **navbar**, a **main content area (`children`)**, and a **footer**.
3. **`{children}`**:
    - **Represents the page content** that will be dynamically inserted.
    - When navigating between pages, **only `{children}` updates**, keeping the layout **persistent** (e.g., Navbar & Footer stay unchanged).