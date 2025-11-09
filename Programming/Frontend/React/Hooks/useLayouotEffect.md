`useLayoutEffect` is a **React Hook** that fires synchronously **after all DOM mutations** but **before the browser paints the screen**. It is similar to `useEffect` but **executes earlier**, making it useful for **reading layout and making immediate updates**.

---

## **🔗 Syntax**

```tsx
useLayoutEffect(() => {
  // Code that runs after DOM updates but before the browser repaints
  return () => {
    // Cleanup function
  };
}, [dependencies]);
```


---

## **📌 How is `useLayoutEffect` Different from `useEffect`?**

|**Feature**|**useEffect**|**useLayoutEffect**|
|---|---|---|
|When it runs|After the browser has painted the screen|Before the browser paints the screen|
|Blocking UI?|**No** (async)|**Yes** (sync, blocks paint)|
|Best for|API calls, logging, subscriptions|Direct DOM manipulations, measurements|
|Example usage|Fetching data, event listeners|Measuring element size, animations|

---

## **🛠️ Example 1: When to Use `useLayoutEffect` Instead of `useEffect`**

```tsx
import { useState, useEffect, useLayoutEffect, useRef } from "react";

export default function Example() {
  const [width, setWidth] = useState(0);
  const divRef = useRef(null);

  useEffect(() => {
    setWidth(divRef.current?.offsetWidth || 0);
  }, []);

  return (
    <div>
      <div ref={divRef} style={{ width: "50vw", height: 100, background: "lightblue" }}>
        Resize me!
      </div>
      <p>Width: {width}px</p>
    </div>
  );
}
```

### **🛑 Problem?**

- The **first render will show `width = 0`** before updating because `useEffect` runs **after** the browser paints.

### **✅ Fix: Using `useLayoutEffect`**

`useLayoutEffect(() => {   setWidth(divRef.current?.offsetWidth || 0); }, []);`

- Now, the width **is set before the browser paints** → No flickering!

---

## **🛠️ Example 2: Preventing Flickering During UI Updates**

Imagine a situation where the UI briefly flashes **before adjusting the layout**.

```tsx
import { useLayoutEffect, useState } from "react";

export default function App() {
  const [isOpen, setIsOpen] = useState(false);

  useLayoutEffect(() => {
    if (isOpen) {
      document.body.style.backgroundColor = "black";
    } else {
      document.body.style.backgroundColor = "white";
    }
  }, [isOpen]);

  return (
    <div>
      <button onClick={() => setIsOpen(!isOpen)}>Toggle Background</button>
    </div>
  );
}
```


### **🔍 What Happens?**

- If we used `useEffect`, the screen **would momentarily flash white** before turning black.
- `useLayoutEffect` **updates the background before the paint**, so no flickering occurs.

---

## **🚀 When Should You Use `useLayoutEffect`?**

✅ **Use `useLayoutEffect` for:**

1. **Reading from and modifying the DOM before paint**
2. **Measuring element sizes and positions**
3. **Synchronized animations**
4. **Preventing UI flickering due to state updates**

❌ **Avoid `useLayoutEffect` for:**

1. **Fetching data (use `useEffect` instead)**
2. **Heavy computations (can block the UI)**

---

## **📌 Common Mistakes & Fixes**

### **❌ Using `useLayoutEffect` for API calls**

`useLayoutEffect(() => {   fetch("/data").then((res) => res.json()).then(setData); }, []);`

**🚨 Problem:** Blocks UI rendering.  
**✅ Fix:** Use `useEffect` instead.

---

## **🎯 Summary**

✔ `useLayoutEffect` runs **before the browser paints** but **after the DOM updates**.  
✔ Use it for **layout calculations, animations, and preventing flickering**.  
✔ Avoid using it for **data fetching or heavy computations**.

Would you like me to optimize your code using `useLayoutEffect`? 🚀