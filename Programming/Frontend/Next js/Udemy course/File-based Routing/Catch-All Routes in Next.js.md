In some cases, you want a **single dynamic route** to handle **any number of path segments**, like:
```bash
/docs/a
/docs/a/b
/docs/a/b/c
```
Instead of creating deeply nested folders manually, you can use a **catch-all route**.


📁 Example File Structure 
```bash
/pages
  └── docs
      └── [...id].js       # Catch-all route
```

### 🛣️ How It Works
- The file name `[...id].js` catches **any number of segments** after `/docs`.
    
- All the segments will be available as an **array** under `router.query.id`.
    
#### URL → Data Mapping:

| URL           | `router.query.id` |
| ------------- | ----------------- |
| `/docs/a`     | `['a']`           |
| `/docs/a/b`   | `['a', 'b']`      |
| `/docs/a/b/c` | `['a', 'b', 'c']` |


## Accessing Catch-All Params
```tsx
import { useRouter } from 'next/router';

const DocsPage = () => {
  const router = useRouter();
  const { id } = router.query; // id is an array

  return (
    <div>
      <h1>Docs Catch-All Route</h1>
      <p>Segments: {JSON.stringify(id)}</p>
    </div>
  );
};

export default DocsPage;

```
🧠 `id` is undefined on first render during server-side rendering, so make sure to guard against that if needed.