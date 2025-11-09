# **🚀 `useRef` in React: A Deep Dive**

`useRef` is a React Hook that provides a **mutable reference** to store values across renders **without triggering re-renders**. It's commonly used for:

1. **Accessing and manipulating DOM elements** 🏗️
2. **Storing values without causing re-renders** 🔒
3. **Keeping track of previous values** ⏳

---

## **🔗 Syntax**

`const myRef = useRef(initialValue);`

- `myRef.current` holds the reference value.
- The value persists across renders without causing re-renders.

---

## **🛠️ Example 1: Accessing & Manipulating the DOM**

One of the most common uses of `useRef` is to directly manipulate a DOM element **without using state**.

```tsx
import { useRef } from "react";

export default function FocusInput() {
  const inputRef = useRef<HTMLInputElement | null>(null);

  const handleFocus = () => {
    if (inputRef.current) {
      inputRef.current.focus();
      inputRef.current.style.backgroundColor = "lightyellow";
    }
  };

  return (
    <div>
      <input ref={inputRef} type="text" placeholder="Click the button to focus" />
      <button onClick={handleFocus}>Focus Input</button>
    </div>
  );
}
```

### **🔍 How It Works?**

- `inputRef.current` **stores a reference to the input element**.
- Clicking the button **focuses the input field** without causing re-renders.

---

## **🛠️ Example 2: Storing Values Without Re-Renders**

Unlike `useState`, updating `useRef.current` **doesn’t trigger re-renders**.

```tsx
import { useRef, useState } from "react";

export default function RefCounter() {
  const [count, setCount] = useState(0);
  const renderCount = useRef(1);

  renderCount.current++;

  return (
    <div>
      <h2>Count: {count}</h2>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <p>Component re-rendered: {renderCount.current} times</p>
    </div>
  );
}
```

### **🔍 Why Use `useRef` Here?**

- `renderCount.current` **persists across renders** without causing a re-render.
- Updating `useState` **triggers a re-render**, but `useRef` **does not**.

---

## **🛠️ Example 3: Keeping Track of Previous Values**

You can use `useRef` to **store the previous state value** before an update.

```tsx
import { useState, useEffect, useRef } from "react";

export default function PreviousValueTracker() {
  const [count, setCount] = useState(0);
  const prevCount = useRef<number | null>(null);

  useEffect(() => {
    prevCount.current = count; // Update previous value AFTER render
  }, [count]);

  return (
    <div>
      <h2>Current Count: {count}</h2>
      <h3>Previous Count: {prevCount.current}</h3>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```
### **🔍 How It Works?**

- `prevCount.current` stores the **previous value** of `count`.
- `useEffect` updates `prevCount.current` **after each render**.

---

## **🛠️ Example 4: Storing Interval IDs or Timers**

A common use case for `useRef` is storing **setInterval IDs** to stop timers when needed.

```tsx
import { useRef, useState } from "react";

export default function Timer() {
  const [count, setCount] = useState(0);
  const timerRef = useRef<NodeJS.Timeout | null>(null);

  const startTimer = () => {
    if (!timerRef.current) {
      timerRef.current = setInterval(() => setCount((c) => c + 1), 1000);
    }
  };

  const stopTimer = () => {
    if (timerRef.current) {
      clearInterval(timerRef.current);
      timerRef.current = null;
    }
  };

  return (
    <div>
      <h2>Count: {count}</h2>
      <button onClick={startTimer}>Start</button>
      <button onClick={stopTimer}>Stop</button>
    </div>
  );
}
```

### **🔍 Why Use `useRef` Here?**

- Stores the **interval ID** across renders **without re-rendering**.
- Prevents unnecessary `useState` updates **just to track the interval**.

---

## **🚀 When Should You Use `useRef`?**

✅ **Use `useRef` for:**

1. **Interacting with the DOM** (e.g., focusing an input)
2. **Storing values across renders** **without triggering re-renders**
3. **Tracking previous state values**
4. **Managing timers, intervals, or external dependencies**

❌ **Avoid `useRef` when:**

1. You need **state updates that should trigger a re-render** (`useState` is better).
2. You want **computed values derived from state** (`useMemo` is better).
3. You need a **function that should not change between renders** (`useCallback` is better).

---

## **📌 Common Mistakes & Fixes**

### **❌ Using `useRef` Instead of `useState`**

```tsx
const countRef = useRef(0);

const increment = () => {
  countRef.current++;
  console.log(countRef.current); // 🛑 UI will NOT update!
};
```

✅ **Fix:** Use `useState` if you need re-renders.

```tsx
const [count, setCount] = useState(0);

const increment = () => setCount(count + 1); // ✅ UI updates correctly
```

---

### **❌ Forgetting to Initialize `useRef` Correctly**

```tsx
const myRef = useRef();
console.log(myRef.current.length); // ❌ Cannot read property 'length' of undefined
```

✅ **Fix:** Always provide an **initial value**.

```tsx
const myRef = useRef<string>("hello");
console.log(myRef.current.length); // ✅ No error
```

---

## **🎯 Summary**

✔ `useRef` **persists values across renders** without causing re-renders.  
✔ It’s great for **DOM manipulation, timers, and storing previous values**.  
✔ If you need **state updates that trigger re-renders**, use `useState` instead.