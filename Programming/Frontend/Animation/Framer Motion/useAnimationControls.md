### **`useAnimationControls` in Framer Motion**

`useAnimationControls` is a hook that allows you to programmatically control animations in Framer Motion. Unlike `animate` which runs automatically based on state changes, `useAnimationControls` lets you start, stop, or update animations manually.

---

### **Code Explanation**

This code creates a **button that triggers a 360° rotation animation** on a `motion.div` when clicked.

---

### **1. Setting Up Animation Controls**

```tsx
const controls = useAnimationControls();
```

- `useAnimationControls()` returns an animation controller (`controls`).
- You can use `controls.start()` to trigger predefined animations.

---

### **2. Click Handler to Start Animation**

```tsx
const onClickHandler = () => {   controls.start("flip"); };
```

- When the button is clicked, `controls.start("flip")` triggers the **"flip" animation** (360° rotation).

---

### **3. Container with Grid Layout**

```tsx
<div
  style={{
    display: "grid",
    placeContent: "center",
    gap: "10px",
    width: "100%",
    height: "100vh",
    backgroundColor: "yellow",
  }}
>
```

- Centers the elements in a **grid layout**.
- `placeContent: "center"` aligns the elements to the middle.
- Background color is yellow.

---

### **4. `motion.div` (Rotating Box)**

```tsx
<motion.div
  style={{
    width: 200,
    height: 200,
    backgroundColor: "white",
  }}
  variants={{
    initial: {
      rotate: "0deg",
    },
    flip: {
      rotate: "360deg",
    },
  }}
  initial="initial"
  animate={controls}
/>

```

- **Variants**:
    - `"initial"`: No rotation (`0deg`).
    - `"flip"`: Rotates **360°**.
- **`animate={controls}`**: The animation is controlled via `useAnimationControls()`.
- The box will remain still until `controls.start("flip")` is called.

---

### **5. `motion.button` (Trigger Button)**

```tsx
<motion.button
  whileHover={{
    scale: 1.123,
    rotate: "-15deg",
  }}
  whileTap={{
    rotate: "15deg",
  }}
  onClick={onClickHandler}
>
  flip
</motion.button>
```

- **`whileHover`**:
    - Increases size (`scale: 1.123`).
    - Rotates counterclockwise (`-15deg`).
- **`whileTap`**:
    - Rotates clockwise (`15deg`).
- **`onClick={onClickHandler}`**:
    - Calls `onClickHandler`, which triggers the `flip` animation.

---

### **How It Works**

1. The box is initially at `rotate: 0deg`.
2. When the **button is clicked**, it calls `controls.start("flip")`.
3. The box **rotates 360°**.
4. The animation only happens **when triggered by the button**.

---

### **Why Use `useAnimationControls`?**

- It **separates animation logic** from state, making it **more flexible**.
- Unlike `animate`, which **depends on state changes**, `useAnimationControls` lets you trigger animations **whenever needed**.
- Useful when you need **more control** over when animations start, stop, or reset.

---

### **Enhancements**

You could modify the code to **toggle the animation** back to `0deg` on subsequent clicks:

tsx

CopyEdit

`const onClickHandler = () => {   controls.start((prev) => (prev === "flip" ? "initial" : "flip")); };`

This way, clicking once **rotates 360°**, and clicking again **resets to 0°**.

Would you like to add more interactions or variations? 🚀