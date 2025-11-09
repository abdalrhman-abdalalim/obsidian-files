1️⃣ **Server Components (Backend Execution)**

- These run **only on the server** (not in the browser).
- They **fetch data**, run database queries, or call APIs **before** sending the HTML to the client.
- The **HTML is generated on the server** and sent as a fully-rendered page.
- **Example:**
	```tsx
	// Server Component (default behavior in Next.js 13+)
	async function Page() {
	  const res = await fetch("https://dummyjson.com/products/1");
	  const product = await res.json();
	  
	  return <h1>{product.title}</h1>;
	}
	
	export default Page;

	```
    
    - This runs on the **server** and sends pre-rendered HTML (`<h1>Product Name</h1>`) to the client.



2️⃣ **Client Components (Browser Execution)**

- These run **only in the browser** and are used for **interactivity** (state, effects, event handlers).
- They receive the **pre-rendered HTML** and **hydrate** it with JavaScript.
- **Example:**
	```tsx
	"use client"; // This makes it a Client Component
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);
  
  return (
    <button onClick={() => setCount(count + 1)}>Count: {count}</button>
  );
}

export default Counter;
```
    - The **button is rendered from the server**, but **clicking it runs JavaScript on the client**.


### 🔥 **Key Takeaways**

- The **server** executes Server Components and sends **pre-rendered HTML**.
- The **client** receives the HTML and hydrates Client Components for **interactivity**.
- **Mixing both** (e.g., using `use client` in components that need interactivity) is the **best practice** in Next.js.

