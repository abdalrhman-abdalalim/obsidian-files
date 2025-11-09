# **🚀 `useMemo` in React: A Deep Dive**

`useMemo` is a **React Hook** that **memorizes the result of a computation** to avoid unnecessary re-renders and improve performance. It is especially useful when dealing with **expensive calculations** or **large data processing**.

---

## **🔗 Syntax**


`const memoizedValue = useMemo(() => computeExpensiveValue(dep1, dep2), [dep1, dep2]);`

- The function inside `useMemo` **only runs when dependencies change**.
- `memoizedValue` **remains unchanged** unless dependencies update.

---

## **📌 Why Use `useMemo`?**

1. **Prevents unnecessary recalculations**
2. **Optimizes performance-heavy computations**
3. **Avoids re-rendering components when values haven’t changed**

---

## **🛠️ Example 1: Optimizing an Expensive Calculation**

Imagine a function that takes a long time to compute.

```tsx
import { useState, useMemo } from "react";

export default function ExpensiveComponent() {
  const [count, setCount] = useState(0);
  const [number, setNumber] = useState(10);

  const expensiveCalculation = (num: number) => {
    console.log("Calculating...");
    for (let i = 0; i < 1e9; i++) {} // Simulating heavy computation
    return num * 2;
  };

  const memoizedResult = useMemo(() => expensiveCalculation(number), [number]);

  return (
    <div>
      <h2>Result: {memoizedResult}</h2>
      <button onClick={() => setCount(count + 1)}>Re-render ({count})</button>
      <button onClick={() => setNumber(number + 1)}>Change Number ({number})</button>
    </div>
  );
}
```


### **🔍 What Happens?**

- Without `useMemo`, `expensiveCalculation` **runs on every render**, even if `count` changes.
- **With `useMemo`**, it **only recalculates when `number` changes**, preventing performance issues.

---

## **🛠️ Example 2: Optimizing Filtered Lists**

Without `useMemo`, filtering a list would run **on every render**, even when unnecessary.

```tsx
import { useState, useMemo } from "react";

export default function ExpensiveComponent() {
  const [count, setCount] = useState(0);
  const [number, setNumber] = useState(10);

  const expensiveCalculation = (num: number) => {
    console.log("Calculating...");
    for (let i = 0; i < 1e9; i++) {} // Simulating heavy computation
    return num * 2;
  };

  const memoizedResult = useMemo(() => expensiveCalculation(number), [number]);

  return (
    <div>
      <h2>Result: {memoizedResult}</h2>
      <button onClick={() => setCount(count + 1)}>Re-render ({count})</button>
      <button onClick={() => setNumber(number + 1)}>Change Number ({number})</button>
    </div>
  );
}
```

### **🔍 What Happens?**

- If we didn’t use `useMemo`, filtering would **recompute on every render**.
- With `useMemo`, filtering **only runs when `query` changes**, improving performance.

---

## **🚀 When Should You Use `useMemo`?**

✅ **Use `useMemo` for:**

1. **Expensive calculations** (e.g., complex math operations, sorting large lists)
2. **Filtering large lists** (e.g., searching through data)
3. **Avoiding unnecessary object recreation** inside dependencies

❌ **Don’t use `useMemo` for:**

1. **Simple values that are cheap to compute**
2. **State updates that don’t affect performance**
3. **Replacing normal state logic (`useState` is better for that)**

---

## **📌 Common Mistakes & Fixes**

### **❌ Using `useMemo` Unnecessarily**

`const memoizedNumber = useMemo(() => number * 2, [number]);`

🚨 **Problem:** Multiplying by 2 is **not an expensive computation**.  
✅ **Fix:** Just compute it normally.

`const normalNumber = number * 2;`

---

## **🎯 Summary**

✔ `useMemo` **stores computed values** and only recalculates when dependencies change.  
✔ Use it for **expensive calculations, filtering, and performance optimizations**.  
✔ Avoid using it for **simple calculations** or where unnecessary.