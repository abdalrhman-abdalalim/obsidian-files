# **🚀 `useCallback` in React: A Deep Dive**

`useCallback` is a **React Hook** that **memorizes a function** to prevent unnecessary re-creation on every render. It is especially useful when passing functions to child components to avoid unnecessary re-renders.

---

## **🔗 Syntax**

`const memoizedCallback = useCallback(() => {   // Function logic here }, [dep1, dep2]);`

- The function inside `useCallback` **only re-creates when dependencies change**.
- `memoizedCallback` is **the same function reference** across renders unless dependencies update.

---

## **📌 Why Use `useCallback`?**

1. **Prevents unnecessary function re-creations**
2. **Optimizes child component re-renders** by keeping the same function reference
3. **Improves performance** in high-frequency updates like event handlers

---

## **🛠️ Example 1: Preventing Unnecessary Re-renders in Child Components**

Without `useCallback`, the `filterNames` function would be **recreated on every render**, causing the child component (`NameList`) to re-render unnecessarily.

```tsx
import { useState, useCallback } from "react";

const names = ["Ahmed", "Mostafa", "Abdo", "Ali", "Mahmoud"];

function NameList({ getFilteredNames }: { getFilteredNames: (query: string) => string[] }) {
  console.log("Child component re-rendered");
  return (
    <ul>
      {getFilteredNames("").map((name) => (
        <li key={name}>{name}</li>
      ))}
    </ul>
  );
}

export default function NameFilter() {
  const [query, setQuery] = useState("");

  const filterNames = useCallback(
    (search: string) => {
      console.log("Filtering names...");
      return names.filter((name) => name.toLowerCase().includes(search.toLowerCase()));
    },
    [] // No dependencies → function never re-created
  );

  return (
    <div>
      <input onChange={(e) => setQuery(e.target.value)} placeholder="Search name..." />
      <NameList getFilteredNames={filterNames} />
    </div>
  );
}
```

### **🔍 What Happens?**

- Without `useCallback`, `filterNames` **would be re-created** on every render.
- Since `filterNames` is passed as a prop, the child component **would re-render unnecessarily**.
- With `useCallback`, the function **keeps the same reference**, preventing re-renders.

---

## **🛠️ Example 2: Optimizing Event Handlers**

Imagine a button that updates a counter. Without `useCallback`, the event handler (`increment`) **gets recreated on every render**.

```tsx
import { useState, useCallback } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);

  const increment = useCallback(() => {
    setCount((prev) => prev + 1);
  }, []); // No dependencies → function remains the same

  return (
    <div>
      <h2>Count: {count}</h2>
      <button onClick={increment}>Increase</button>
    </div>
  );
}
```

### **🔍 What Happens?**

- Without `useCallback`, `increment` is recreated **on every render**, even though its logic doesn’t change.
- With `useCallback`, the function reference **stays the same**, improving performance.

---

## **🛠️ Example 3: Combining `useCallback` with `useMemo`**

You can **combine `useCallback` with `useMemo`** to optimize both function and computed value memoization.

```tsx
import { useState, useCallback, useMemo } from "react";

const numbers = [1, 2, 3, 4, 5];

export default function MemoizedComponent() {
  const [factor, setFactor] = useState(2);

  const multiplyNumbers = useCallback(
    () => numbers.map((num) => num * factor),
    [factor] // Only re-creates when `factor` changes
  );

  const memoizedNumbers = useMemo(() => multiplyNumbers(), [multiplyNumbers]);

  return (
    <div>
      <h2>Numbers: {memoizedNumbers.join(", ")}</h2>
      <button onClick={() => setFactor(factor + 1)}>Increase Factor ({factor})</button>
    </div>
  );
}

```

### **🔍 What Happens?**

- `multiplyNumbers` **only changes when `factor` updates** (thanks to `useCallback`).
- `memoizedNumbers` **only recomputes when `multiplyNumbers` changes** (thanks to `useMemo`).
- **Prevents unnecessary calculations and re-renders.**

---

## **🚀 When Should You Use `useCallback`?**

✅ **Use `useCallback` for:**

1. **Passing functions to child components** to prevent re-renders
2. **Optimizing event handlers** in components that re-render frequently
3. **Memoizing expensive functions** that would otherwise be recreated

❌ **Avoid `useCallback` when:**

1. **The function is simple and doesn’t cause performance issues**
2. **State updates happen inside the same component** (no need to pass it down)
3. **Overusing it** can actually hurt performance due to memory usage

---

## **📌 Common Mistakes & Fixes**

### **❌ Using `useCallback` Without Dependencies**

``const increment = useCallback(() => {   setCount(count + 1); }, []); // ❌ `count` is not included in dependencies``

🚨 **Problem:** `count` inside `useCallback` **never updates**.  
✅ **Fix:** Add `count` as a dependency.

`const increment = useCallback(() => {   setCount((prev) => prev + 1); }, []);`

---

## **🎯 Summary**

✔ `useCallback` **stores function references** and only re-creates when dependencies change.  
✔ Use it for **optimizing event handlers and preventing unnecessary re-renders in child components**.  
✔ Avoid overusing it where unnecessary, as it can consume memory.