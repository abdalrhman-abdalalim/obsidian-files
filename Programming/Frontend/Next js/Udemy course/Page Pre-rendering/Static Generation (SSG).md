### 🧾 What It Is

- Pages are **pre-rendered at build time**.
    
- Resulting HTML is **cached and reused** for all requests.
    

### 📈 SEO Impact

- Provides fully-rendered, crawlable HTML.
    
- Improves indexing and ranking.
    

### 🟢 Use Cases

- Marketing pages
    
- Blogs
    
- Portfolios
    
- Product listings
    
- Any data that doesn’t change frequently
    

---

## 📦 `getStaticProps` in Next.js

## Why We Use `getStaticProps`

`getStaticProps` is a Next.js function that runs at build time to pre-render pages. Here's why it's valuable:

1. **Static Generation**: The page is generated at build time, making it very fast to serve to users.
    
2. **Data Fetching**: It allows you to fetch data before the page is rendered, so the page is served with all data ready.
    
3. **Performance**: Since the page is pre-rendered, there's no need for client-side data fetching, leading to faster page loads.
    
4. **SEO Benefits**: Search engines can crawl the pre-rendered HTML content easily since it doesn't require JavaScript execution.
    
5. **Type Safety**: With TypeScript, we can define the shape of our props and get compile-time checking.

### 🧑‍💻 Usage Example

```tsx
export async function getStaticProps() {
  const data = await fetch('https://api.example.com/posts').then(res => res.json());

  return {
    props: { posts: data },
    revalidate: 60, // Optional: ISR
  };
}

function Blog({ posts }) {
  return (
    <ul>
      {posts.map(post => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  );
}

export default Blog;

```


### 🕒 When to Use

- Data is **public** and available at **build time**.
    
- Content **rarely changes** or can be **revalidated occasionally**.
    
- SEO is a **high priority** (e.g., blogs, landing pages).
    

---

## ⏳ Incremental Static Regeneration (ISR)

- Use `revalidate` in `getStaticProps` to **regenerate static pages** in the background.
    
- Best for **data that changes occasionally**.
    

---

## ❌ Avoid `getStaticProps` If:

- Data changes frequently.
    
- Pages need **real-time data** or **user-specific content**.
    

---

## 🆚 Quick Comparison Table

|Feature|React (CSR)|Next.js (SSG)|
|---|---|---|
|Rendering Time|Client-side|Build time|
|SEO|Poor|Excellent|
|Data Fetching|useEffect / SWR|getStaticProps|
|Best For|Dynamic apps|Static content|
|HTML on Load|Empty shell|Fully pre-rendered|
|Performance|Slower (more JS)|Faster (CDN-ready)|
