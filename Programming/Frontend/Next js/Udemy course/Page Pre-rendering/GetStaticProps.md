In **Next.js**, `getStaticProps` is used to fetch data **at build time** for a page, allowing you to generate static pages with dynamic content.
### 📥 Parameters – `context`
`getStaticProps(context)` receives a `context` object which can contain:
- `params`: The route parameters (only available if the page uses **dynamic routing**).
- `locale`, `locales`, `defaultLocale`: Used for internationalized routing.
### 1. **`notFound` and `redirect` Returns**
These are special return options for handling missing data or redirects:
```tsx
export async function getStaticProps(context) {
  // Fetch data
  const data = await fetchData();

  // Case 1: Page not found (404)
  if (!data.exists) {
    return { 
      notFound: true // Will render 404 page
    };
  }

  // Case 2: Redirect
  if (data.isMoved) {
    return {
      redirect: {
        destination: '/new-url',
        permanent: false // 307 temp redirect (true=301 permanent)
      }
    };
  }

  // Normal case
  return {
    props: { data },
    revalidate: 60
  };
}
```

### 2. **`context` Parameter**
The context contains useful values, especially for dynamic routes:
```tsx
// For pages like `/posts/[slug].js`
export async function getStaticProps(context) {
  // Access route params
  const { params } = context;
  const { slug } = params; // Gets value from URL

  // Other context properties:
  const locale = context.locale; // i18n
  const preview = context.preview; // Preview mode

  const post = await getPostBySlug(slug);

  return { 
    props: { post },
    revalidate: 10
  };
}
```