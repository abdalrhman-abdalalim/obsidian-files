### 1. **`getStaticProps` (Server-Side)**
```tsx
// pages/products/[productId].js
export async function getStaticProps(context) {
  // Access during pre-rendering (Node.js environment)
  const { productId } = context.params; 

  // Fetch data server-side
  const product = await fetchProduct(productId);

  return { 
    props: { product }, // Passed to the page component
    revalidate: 60 
  };
```
**When it runs:**
- At **build time** (or during ISR revalidation)
- In the **Node.js environment** (server/SSG)

**Use cases:**
- Pre-render pages with dynamic data
- SEO optimization (content visible in initial HTML)
- Access sensitive data (API keys, etc.)

### 2. **`useRouter` (Client-Side)**
```tsx
// Inside your React component
import { useRouter } from 'next/router';

export default function ProductPage({ product }) {
  // Access in the browser (client-side)
  const router = useRouter();
  const { productId } = router.query; 

  // Client-side logic (e.g., analytics)
  useEffect(() => {
    if (productId) logViewEvent(productId);
  }, [productId]);

  return <div>{product.name}</div>;
  }
```
**When it runs:**
- After the page loads **in the browser**
- During **client-side navigation** (e.g., `next/link`)

**Use cases:**
- Client-side effects (analytics, animations)
- Dynamic UI updates (without full page reload)
- Accessing post-hydration route changes