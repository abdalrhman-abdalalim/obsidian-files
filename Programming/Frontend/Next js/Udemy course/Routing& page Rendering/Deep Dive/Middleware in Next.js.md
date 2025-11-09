### 🧩 What is Middleware?

Middleware allows you to **run code before a request reaches the page**. It can intercept requests to add logic like **authentication checks**, **data fetching**, **request logging**, or **redirects**.

- ✅ Middleware runs on the server side.
    
- ✅ Middleware functions run before any route handlers or page rendering happens.
    

---

### 📁 File Structure for Middleware

`beside jsconfig.json -> middleware.ts`

In Next.js, **middleware** is usually placed in the `app/` or `pages/` directory as `middleware.ts` or `middleware.js`.

---

### ⚙️ Example: Simple Redirect Middleware

Let's say you want to redirect users who aren't logged in to a login page.

```tsx
// app/middleware.ts
import { NextResponse } from 'next/server';
import type { NextRequest } from 'next/server';

export function middleware(req: NextRequest) {
  const isLoggedIn = Boolean(req.cookies.get('authToken'));

  if (!isLoggedIn) {
    return NextResponse.redirect(new URL('/login', req.url));
  }

  return NextResponse.next(); // Allow the request to continue
}

export const config = {
  matcher: ['/dashboard', '/profile'], // Apply to specific routes
};
```

- `NextResponse.redirect(url)` is used for redirection.
    
- `NextResponse.next()` lets the request continue if no action is needed.
    

---

### 🧠 Example: Adding Custom Headers

You can modify requests or responses before the page renders. Here's how to add custom headers to all requests:

```tsx
// app/middleware.ts
import { NextResponse } from 'next/server';

export function middleware(req) {
  const response = NextResponse.next();
  response.headers.set('X-Custom-Header', 'Hello from middleware');
  return response;
}

export const config = {
  matcher: '/api/*', // Apply to API routes
};
```

---

### 🎯 When to Use Middleware?

- **Authentication & Authorization**: Check if the user is logged in before accessing sensitive routes.
    
- **Redirects**: Redirect users based on conditions like device type, user roles, etc.
    
- **Headers or Cookies**: Add custom headers or modify cookies for specific requests.
    
- **Performance Tracking**: Measure the performance of specific API routes or pages.
    

---

### ✅ Best Practices for Middleware

1. **Use `NextResponse.next()`** to pass control to the next middleware or route handler.
    
2. **Minimize logic in middleware**: Complex logic in middleware can slow down response times.
    
3. **Apply middleware selectively**: Use the `config.matcher` property to limit where middleware runs.
    

---

### 🧭 Middleware Configurations

- **`matcher`**: Defines which routes the middleware should apply to.
    

Example:

```tsx
export const config = {
  matcher: ['/dashboard/*', '/profile/*'], // Only run middleware for these routes
};

```

- **`regions`** (Next.js 13.4+): Enables custom regions for middleware to run in specific parts of the world.
    

Example:

```tsx
export const config = {
  regions: ['US', 'EU'], // Apply middleware for US and EU only
};

```


---

### 🚫 Limitations of Middleware

- **No state persistence**: Middleware can't maintain state across requests. If you need to share data, use headers, cookies, or sessions.
    
- **Performance**: Heavy computations in middleware may slow down page loads, so keep it lightweight.