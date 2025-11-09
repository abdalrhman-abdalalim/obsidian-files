While `getStaticProps` generates pages at **build time**, `getServerSideProps` runs **on every request**, making it ideal for dynamic content that changes frequently or requires access to the incoming request (e.g., cookies, headers, or real-time data).

## **Key Differences: `getServerSideProps` vs. `getStaticProps`**

|Feature|`getServerSideProps` (SSR)|`getStaticProps` (SSG)|
|---|---|---|
|**When it runs**|**On every request** (server-side)|**At build time** (or ISR revalidation)|
|**Performance**|Slower (no caching by default)|Faster (pre-rendered, CDN-cached)|
|**Use Case**|Real-time data, auth, personalization|Static content, SEO optimization|
|**Access to `req`/`res`**|Yes (full request/response objects)|No|
|**Caching**|Possible via `Cache-Control` headers|Built-in (ISR)|
## **How `getServerSideProps` Works**
### **1. Basic Syntax**
```tsx
export async function getServerSideProps(context) {
  // Access request/response objects
  const { req, res } = context;
  
  // Fetch data on every request
  const data = await fetchData(req.headers.cookie);

  return {
    props: { data }, // Pass data to the page
  };
}
```

### **2. Accessing Request-Specific Data**
Since it runs per request, you can:

- Check **cookies** (authentication)
- Read **headers** (user-agent, geo-location)
- Handle **query parameters** dynamically.

```tsx
export async function getServerSideProps({ req }) {
  const user = await getUserFromToken(req.cookies.token);
  
  if (!user) {
    return { redirect: { destination: '/login', permanent: false } };
  }

  return { props: { user } };
}
```

### **3. Dynamic Routing (Same as `getStaticProps`)**
```tsx
// pages/blog/[slug].js
export async function getServerSideProps({ params }) {
  const post = await getPostBySlug(params.slug);
  
  if (!post) {
    return { notFound: true }; // Show 404
  }

  return { props: { post } };
}
```

## **When to Use `getServerSideProps`?**

✅ **Real-time data** (e.g., stock prices, live scores)  
✅ **User authentication** (personalized pages)  
✅ **Access to `req`/`res`** (cookies, headers, geolocation)  
❌ **Not needed for static content** (use `getStaticProps` instead)

## **Performance Consideration**

- **Slower than static generation** (no pre-rendering).
    
- **Use caching headers** to optimize:
```tsx
export async function getServerSideProps({ req, res }) {
  res.setHeader('Cache-Control', 'public, s-maxage=10, stale-while-revalidate=59');
  return { props: { data } };
}
```


## **Full Example: SSR with Authentication**
```tsx
// pages/dashboard.js
export async function getServerSideProps({ req }) {
  // Check auth token
  const token = req.cookies.token;
  if (!token) {
    return { redirect: { destination: '/login', permanent: false } };
  }

  // Fetch user-specific data
  const user = await fetchUserData(token);
  const latestOrders = await fetchOrders(token);

  return { 
    props: { user, orders: latestOrders },
  };
}

export default function Dashboard({ user, orders }) {
  return (
    <div>
      <h1>Welcome, {user.name}</h1>
      <OrdersList data={orders} />
    </div>
  );
}
```