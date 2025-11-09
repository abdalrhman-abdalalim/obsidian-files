`whileInView` is a prop in Framer Motion that **triggers an animation when an element enters the viewport**. It is commonly used for scroll-based animations, ensuring elements animate only when they become visible.

#### **Key Features of `whileInView`:**

1. **Runs once by default** when the element enters the viewport.
2. **Can be configured** to re-trigger if the element leaves and re-enters.
3. **Works well for lazy animations**, making pages more interactive.

---
### **Code Explanation**

This code creates a scroll-based animation where:

- A red `motion.div` fades in when scrolled into view (`whileInView`).
- A second `div` changes color dynamically based on whether it's in view.

---

### **1. `useRef` & `useInView` for View Detection**

```tsx
const ref = useRef(null); const isInView = useInView(ref);
```

- `useRef(null)`: Creates a reference for the second `div`.
- `useInView(ref)`: Checks if the `ref` element is currently **visible in the viewport**.

---

### **2. Running an Animation When Visible**

```tsx
useEffect(() => {
  if (isInView) {
    controls.start("visible");
  }
}, [isInView]);
```

- **When `isInView` becomes `true`**, it triggers an animation using `controls.start("visible")`.
- The effect runs **whenever `isInView` changes**.

---

### **3. Scrollable Container**

```tsx
<div style={{
  height:"200vh"
}}>
```

- Makes the page **tall** (`200vh` height) so scrolling is required.
- This allows elements to enter and leave the viewport naturally.

---

### **4. Red `motion.div` (Fades In on Scroll)**

```tsx
<motion.div style={{
  height: "100vh",
  background:"red"
}}
  initial={{
    opacity: 0
  }}
  whileInView={{
    opacity: 1
  }}
  transition={{
    duration: 0.4,
    ease:"easeIn"
  }}
/>
```

- **Starts with `opacity: 0`** (hidden).
- **When scrolled into view**, `opacity` animates to `1`.
- **Uses `transition`** to control speed (`0.4s`) and easing.

---

### **5. Color-Changing `div`**

```tsx
<div ref={ref} style={{
  height: "50vh",
  background: isInView ? "green" : "yellow",
  transition:"1s background"
}}></div>
```

- Uses `ref={ref}` so `useInView` can track visibility.
- **Background color changes**:
    - **Green** if in view.
    - **Yellow** if out of view.
- **Smooth transition** (`1s`) when color changes.

---

### **How It Works**

1. **Scroll down** → The red box **fades in** (`whileInView`).
2. **Scroll further** → The second `div` **turns green** when in view.
3. **Scroll up (out of view)** → The second `div` **turns yellow** again.

---

### **Why Use `whileInView`?**

✅ **Lightweight:** No need for extra state or event listeners.  
✅ **Automatic:** Animations trigger only when needed.  
✅ **Great for Scroll Animations:** Lazy loads elements smoothly.


---

`useScroll()` is a hook provided by **Framer Motion** that helps track how far the user has scrolled on a page. It provides reactive values that update in real-time as the user scrolls.

---

