## 📍 Intercepted Navigation & Intercepted Routing in Next.js

### 🔄 What is Intercepted Routing?

Intercepted routes allow you to **display content like a modal** over another page without leaving the underlying page. For example, opening a modal when clicking on a card, instead of navigating to a full new page.

This is achieved using **intercepted segments** (e.g., `(@modal)/news/[slug]`) and wrapped in a layout that handles both the original page content and the modal UI.

---

### 🧱 Folder Structure & Route Setup

To implement intercepted routing, you typically organize your files like this:

```css
app/
├─ news/
│  ├─ page.tsx (main content)
├─ (modal)/
│  ├─ news/
│  │  ├─ [slug]/
│  │  │  ├─ page.tsx (modal content)
├─ layout.tsx (wraps page + modal)
```

🚫 **Important**: When switching from **intercepted** routes to **parallel** routes, **you do _not_ change the single dot (`.`) to double dots (`..`)**. That's because parallel route folders (e.g., `(modal)`) are **ignored** in the URL path—they don't affect routing like parent folders do.

---

### 🧾 `page.tsx` in Intercepted Route

The `page.tsx` file inside the intercepted route folder handles modal rendering. It uses `params` to access the slug and render the modal with backdrop and content.

```tsx
import BackDrop from "@/components/BackDrop";
import { DUMMY_NEWS } from "@/dummy-news";
import { notFound } from "next/navigation";

interface IProps {
  params: Promise<{ slug: string }>;
}

const page = async ({ params }: IProps) => {
  const { slug } = await params;

  const newData = DUMMY_NEWS.find((news) => news.slug === slug);
  if (!newData) {
    notFound(); // Redirects to not-found.tsx if data doesn't exist
  }

  return (
    <div className="fixed inset-0 z-50 flex items-center justify-center">
      {/* Backdrop */}
      <BackDrop />
      {/* Modal Dialog */}
      <div className="relative z-10 w-full max-w-2xl p-6 bg-white rounded-xl shadow-lg dark:bg-zinc-900">
        <h2 className="mb-4 text-xl font-semibold text-black dark:text-white">
          This is an Intercepted Route
        </h2>
        <div className="w-full h-auto overflow-hidden rounded-lg">
          <img
            src={`/images/news/${newData?.image}`}
            alt={newData?.title}
            className="object-cover w-full h-full"
          />
        </div>
        <p className="mt-4 text-gray-700 dark:text-gray-300">
          {newData?.title}
        </p>
      </div>
    </div>
  );
};
export default page;
```

### ✅ Key Concepts Recap

- **Intercepted navigation** allows showing a modal or sidebar without leaving the current page.
    
- The `layout.tsx` wraps the `children` (main content) and `modal` (intercepted content).
    
- You **don't change the dot** in intercepted routes when using parallel routes.
    
- The intercepted route's `page.tsx` handles modal UI and uses `params` to fetch relevant data.
    
- Use `notFound()` for fallback when a slug is invalid.