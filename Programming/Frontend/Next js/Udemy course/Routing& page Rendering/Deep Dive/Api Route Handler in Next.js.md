API Routes in Next.js allow you to build **backend functionality** directly inside your app. These routes live under the `app/api` or `pages/api` directory and handle **HTTP requests** (GET, POST, etc).

- ✅ Can be used for form handling, data processing, authentication, etc.
    
- ✅ Server-side only – no exposure to the client.


### 🧠 Example: Handling POST with Body

```tsx
// app/api/contact/route.ts

import { NextResponse } from "next/server";

export async function POST(req: Request) {
  const body = await req.json();

  if (!body.name || !body.email) {
    return NextResponse.json({ error: "Missing fields" }, { status: 400 });
  }

  return NextResponse.json({ success: true, data: body });
}
```

### 🆚 `pages/api` vs `app/api`

|Feature|`pages/api` (Pages Router)|`app/api` (App Router)|
|---|---|---|
|Directory|`/pages/api`|`/app/api`|
|Exports|Default function|Named functions: `GET`, `POST`, etc.|
|Middleware support|✅|✅|
|Built-in streaming|❌|✅|
|Server functions|❌|✅ (using `NextResponse`)|