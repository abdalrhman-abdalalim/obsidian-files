# **🔥 `useEffect` in React: The Ultimate Guide**

`useEffect` is a React Hook that allows you to **perform side effects** in function components, such as:  
✅ Fetching data from an API  
✅ Updating the DOM  
✅ Subscribing to events  
✅ Setting up timers

---

## **📌 Syntax**

```tsx
useEffect(() => {
  // Side effect logic here
  return () => {
    // Cleanup logic (optional)
  };
}, [dependencies]);
```


- The **first argument** is a function that runs the effect.
- The **second argument** is the dependency array (`[]`):
    - `[]` → Runs **only once** (on mount).
    - `[variable]` → Runs when **variable changes**.
    - No dependency array → Runs **on every render**.

---

## **🛠️ Example 1: `useEffect` for Fetching Data**

```tsx
import { useState, useEffect } from "react";

export default function UsersList() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((response) => response.json())
      .then((data) => setUsers(data));
  }, []); // Empty dependency array → Runs once on mount

  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

### **🔍 What’s Happening?**

✔ `useEffect` runs **once on mount**, fetches user data, and updates state.  
✔ When state updates, React **re-renders** the component to display users.

---

## **🛠️ Example 2: `useEffect` with Dependencies**

```tsx
import { useState, useEffect } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `Count: ${count}`;
  }, [count]); // Runs when `count` changes

  return (
    <div>
      <h2>Count: {count}</h2>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>
  );
}
```

### **🔍 What’s Happening?**

✔ When `count` changes, `useEffect` updates the **document title**.  
✔ If `count` doesn’t change, the effect **does not re-run**, optimizing performance.

---

## **🛠️ Example 3: Cleanup with `useEffect` (Event Listeners)**

```tsx
import { useState, useEffect } from "react";

export default function WindowWidth() {
  const [width, setWidth] = useState(window.innerWidth);

  useEffect(() => {
    const handleResize = () => setWidth(window.innerWidth);
    window.addEventListener("resize", handleResize);

    return () => {
      window.removeEventListener("resize", handleResize); // Cleanup on unmount
    };
  }, []);

  return <h2>Window width: {width}px</h2>;
}
```

### **🔍 What’s Happening?**

✔ When the component mounts, it listens for `resize` events.  
✔ When the component **unmounts**, the event listener is removed to **prevent memory leaks**.

---

## **🛠️ Example 4: `useEffect` with setTimeout (Polling)**

```tsx
import { useState, useEffect } from "react";

export default function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setSeconds((prev) => prev + 1);
    }, 1000);

    return () => clearInterval(interval); // Cleanup on unmount
  }, []);

  return <h2>Seconds: {seconds}</h2>;
}
```


### **🔍 What’s Happening?**

✔ A timer increases `seconds` every **1 second**.  
✔ The `clearInterval(interval)` **stops the timer** when the component unmounts.

---

## **🚀 Common Mistakes & Fixes**

### **❌ Forgetting the Cleanup Function**

```tsx
useEffect(() => {
  window.addEventListener("resize", () => console.log("Resized!"));
}, []); // ❌ Memory leak: Listener never removed!
```

✅ **Fix:** Always clean up event listeners inside `useEffect`:

```tsx
useEffect(() => {
  const handleResize = () => console.log("Resized!");
  window.addEventListener("resize", handleResize);

  return () => window.removeEventListener("resize", handleResize);
}, []);
```

---

### **❌ Updating State Without a Dependency Array**

``useEffect(() => {   setCount(count + 1); }, []); // ❌ `count` is always the initial state (0)``

✅ **Fix:** Include `count` in the dependency array:

``useEffect(() => {   setCount(count + 1); }, [count]); // ✅ Runs when `count` changes``

---

### **❌ Unnecessary Re-Renders**

`useEffect(() => {   console.log("Runs on every render!"); });`

✅ **Fix:** Add dependencies or an empty array (`[]`) to control execution.

---

## **🎯 When to Use `useEffect`?**

✅ **Use `useEffect` when:**

- You need to fetch data from an API (`fetch`, `axios`).
- You want to **update the DOM** (e.g., `document.title`).
- You need to **subscribe to events** (e.g., `window.addEventListener`).
- You want to start an **interval or timeout**.

❌ **Avoid `useEffect` when:**

- You can compute the value **inside the render function**.
- You’re updating **state in a way that causes an infinite loop**.

---

## **🎯 Summary**

✔ `useEffect` **performs side effects** in function components.  
✔ Runs **on mount**, **on update**, or **on unmount** (with cleanup).  
✔ Useful for **API calls, event listeners, and timers**.  
✔ Avoid common **performance issues** by managing dependencies correctly.