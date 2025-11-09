## 🔎 Understanding Search Params in Next.js

Search params in Next.js allow you to access dynamic route parameters and query strings in Server Components, Server Actions, and Route Handlers. This is useful when handling URLs like `/products/shoes` or `/blog/my-first-post` as well as query strings like `/?mode=signup`.

### 📋 Accessing Search Params

You can access search params using the `useSearchParams()` hook in Client Components or the `new URL()` API in Server Components.

### 📝 Example - Reading a Single Param

```
'use client';
import { useSearchParams } from 'next/navigation';

export default function MyComponent() {
  const searchParams = useSearchParams();
  const mode = searchParams.get('mode');

  return <div>Current Mode: {mode}</div>;
}
```

### 📝 Example - Reading Params on the Server

```
import { NextRequest } from 'next/server';

export function middleware(req: NextRequest) {
  const url = new URL(req.url);
  const mode = url.searchParams.get('mode');
  console.log('Mode:', mode);
}
```

### ⚠️ Key Points

- Always `await` `params` when using Next.js 15+.
    
- Use `useSearchParams()` in Client Components.
    
- Use the `URL` API in Server Components and Middleware.
    
- Be aware that search params are part of the URL, so they are publicly accessible.