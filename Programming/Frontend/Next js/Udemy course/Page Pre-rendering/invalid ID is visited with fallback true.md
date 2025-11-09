## ❓ What happens if an invalid ID is visited with `fallback: true`

### Scenario:
- You use `fallback: true` in `getStaticPaths`
- A user visits a page with a **non-existent ID** like `/product/invalid123`
- The page isn’t pre-rendered, so Next.js tries to **generate it on-demand** using `getStaticProps`

### But... if you don’t handle that invalid ID in `getStaticProps`, it might:
- ❌ Crash the page
- ❌ Show broken UI
- ❌ Or worse, show `undefined` data\

```tsx
// pages/product/[id].tsx

export async function getStaticPaths() {
  return {
    paths: [], // Optional: can include most common ones
    fallback: true, // or "blocking"
  };
}

export async function getStaticProps({ params }) {
  const { id } = params;

  const product = await fetchProductById(id); // Assume this hits DB or API

  if (!product) {
    return {
      notFound: true, // ⛔ Show 404 if ID is invalid
    };
  }

  return {
    props: { product },
    revalidate: 60, // optional: for ISR
  };
}

```