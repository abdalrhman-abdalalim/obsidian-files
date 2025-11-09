To access route data like parameters or the current path, use the `useRouter` hook from `next/router`.

```tsx
import { useRouter } from 'next/router';

const ProductDetail = () => {
  const router = useRouter();

  console.log(router.pathname);        // Output: '/products/[id]'
  console.log(router.query);           // Output: { id: '123' } (if URL is /products/123)

  return <div>Product ID: {router.query.id}</div>;
};

```

### 🧠 `useRouter()` Details

|Property|Description|
|---|---|
|`router.pathname`|Returns the route pattern (e.g. `/products/[id]`)|
|`router.query`|Returns an object with the actual dynamic route parameters (e.g. `{ id: "123" }`)|
This is useful when your URL contains query parameters or dynamic segments like:
```bash
/dashboard?projectId=5
```
You can access it like:
```tsx
const router = useRouter();
console.log(router.query.projectId); // Outputs: "5"
```


