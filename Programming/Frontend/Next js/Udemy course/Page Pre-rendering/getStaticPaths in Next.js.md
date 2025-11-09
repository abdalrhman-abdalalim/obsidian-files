When you're working with **dynamic routes** (like `/product/[id]`), Next.js needs to know **which `id` values to pre-render** during the build process.

> Static pages don’t just need data — they also need to know **which dynamic routes exist**.

## 🔁 What `getStaticPaths` Does

It allows you to define which dynamic paths should be **pre-generated at build time**.
```tsx
export async function getStaticPaths() {
  // Fetch all possible IDs (e.g., from an API/database)
  const products = await fetchAllProductIds();
  
  // Map to the required `params` format
  const paths = products.map((product) => ({
    params: { id: product.id.toString() },
  }));

  return { 
    paths, 
    fallback: true // or 'blocking' or false
  };
}

export async function getStaticProps({ params }) {
  // Fetch data for a specific ID
  const product = await fetchProductData(params.id);
  return { props: { product } };
}
```

### 2. **How Pre-Rendering Works (Behind the Scenes)**

Behind the scenes, Next.js **fetches the data for each path** using `getStaticProps`, then saves the result into **JSON files**. These files are later **read and injected** when someone visits the page.

- **At build time**, Next.js:
    1. Calls `getStaticPaths` to get all `paths`.
    2. For each path, calls `getStaticProps` and generates a static HTML + JSON file (e.g., `products/1.json`).
    3. Stores these files in the `.next/server/pages` directory.
        
- **When a user visits `/products/1`**:
    - Next.js serves the pre-built HTML.
    - The React component hydrates using data from the JSON file.

## 🧩 What is `fallback`?

Sometimes, you have **too many possible paths** — some are rarely visited. In that case, generating all of them at build time is a waste.

That’s where the `fallback` option comes in:
### ➤ `fallback: false`
- ✅ Only the paths listed in `paths[]` will be pre-rendered.
- ❌ Any other path will return a **404**.
- ⚡ Very fast — all pages are built ahead of time.

---
### ➤ `fallback: true`
- ✅ Paths **not in `paths[]`** will be generated **on the first request**.
- ⏳ The user will see a **loading spinner** or fallback UI while the page is being built.
- 🗂️ Once generated, the page is cached and served like a normal static page.

> ✅ Good for large apps where only a few pages are visited often.

---
### ➤ `fallback: "blocking"`
- ✅ Same as `true`, but **no loading UI**.
- ⛔ The request is **blocked** until the page is fully generated.
- 📈 Better for SEO or critical content.

> ❗ First load may take longer, but the user gets the **full content immediately**.


### 4. **Why Use `fallback: true` or `'blocking'`?**

- **Avoid slow builds**: Pre-rendering 10,000 pages at build time is impractical.
- **Handle rare paths**: For paths like `/products/old-seasonal-item`, generate only when requested.
- **Dynamic content**: New content added after build (e.g., CMS updates) can still be rendered.

### 5. **Deep Dive: `fallback: true`**
- **First request**:
    - Returns a "fallback" version of the page (e.g., with a loading spinner).
    - Next.js generates the page in the background.
        
- **Subsequent requests**:
    - Serves the statically generated page.
        
- **UI Handling**:
```tsx
import { useRouter } from 'next/router';

function ProductPage({ product }) {
  const router = useRouter();

  if (router.isFallback) {
    return <div>Loading...</div>; // Show a loader
  }

  return <div>{product.name}</div>;
}
```


### 6. **`fallback: 'blocking'`**

- **Behavior**:
    - The server generates the page **on first request** (no loading state).
    - The user waits until the page is fully rendered.
        
- **Pros**:
    - Better for SEO (no "loading" flash).
    - Simpler code (no `isFallback` checks).
        
- **Cons**:
    - Slower initial response if the page wasn’t pre-rendered.


❓ What happens if an