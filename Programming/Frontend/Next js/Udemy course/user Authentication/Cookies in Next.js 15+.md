## 📦 Importing Cookies

```
import { cookies } from 'next/headers';
```

## 🔄 Reading Cookies

The `cookies()` function is asynchronous, allowing you to read the incoming request cookies in **Server Components** and read/write outgoing cookies in **Server Actions** or **Route Handlers**.

### 📋 Example:

```
import { cookies } from 'next/headers';

export default async function Page() {
  const cookieStore = await cookies();
  const theme = cookieStore.get('theme');
  return '...';
}
```

### 📝 Available Methods

|Method|Return Type|Description|
|---|---|---|
|`get(name)`|Object|Returns an object with the name and value of the specified cookie.|
|`getAll()`|Array|Returns an array of all the cookies as objects.|
|`has(name)`|Boolean|Returns `true` if the specified cookie exists, `false` otherwise.|
|`set(name, value, options)`|-|Sets a cookie with the specified name, value, and options.|
|`delete(name)`|-|Deletes the specified cookie. (Only in Server Actions or Route Handlers)|
|`clear()`|-|Deletes all cookies.|
|`toString()`|String|Returns a string representation of the cookies.|

### 🔧 Setting Cookies

```
await cookies().set('userToken', 'abc123', {
  maxAge: 60 * 60 * 24 * 7,  // 7 days
  path: '/',
  secure: true,
  httpOnly: true,
  sameSite: 'Strict',
});
```

### 🔑 Options

|   |   |   |
|---|---|---|
|Option|Type|Description|
|`name`|String|Specifies the name of the cookie.|
|`value`|String|The value to store in the cookie.|
|`expires`|Date|The exact date when the cookie will expire.|
|`maxAge`|Number|The cookie’s lifespan in seconds.|
|`domain`|String|The domain where the cookie is available.|
|`path`|String|Limits the cookie's scope to a specific path (default: `/`).|
|`secure`|Boolean|Ensures the cookie is sent only over HTTPS.|
|`httpOnly`|Boolean|Restricts the cookie to HTTP requests only.|
|`sameSite`|Boolean, 'lax', 'strict', 'none'|Controls cross-site request behavior.|
|`priority`|String ('low', 'medium', 'high')|Specifies the cookie's priority.|
|`encode`|Function|Function to encode the cookie's value.|
|`partitioned`|Boolean|Indicates if the cookie is partitioned.|

## ⚠️ Notes

- **Asynchronous Behavior:** `cookies()` is an async function. You must use `await` or React's `use()` to access it.
    
- **Dynamic Rendering:** Using `cookies()` in a page or layout opts the route into dynamic rendering.
    
- **Legacy Synchronous Access:** Synchronous access is still possible in Next.js 15 for backward compatibility but will be deprecated soon.
    
- **Cookie Deletion Restrictions:** The `.delete()` method can only be called in a **Server Action** or **Route Handler**, on the same domain and protocol as the cookie being deleted.
    
- **Streaming Limitation:** HTTP does not allow setting cookies after streaming starts, so `.set()` must be used early in the server response cycle.
    

## 🚀 Best Practices

- Use `secure` and `httpOnly` for sensitive data to enhance security.
    
- Keep cookie lifetimes short for better control over data.
    
- Use `sameSite` to prevent Cross-Site Request Forgery (CSRF) attacks.