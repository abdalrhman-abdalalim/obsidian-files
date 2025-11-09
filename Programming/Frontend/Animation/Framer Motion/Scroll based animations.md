#### **1. `useScroll()` (Framer Motion)**

```tsx 
const { scrollYProgress } = useScroll();
```

- This **tracks the vertical scroll progress** as a value from `0` (top of the page) to `1` (bottom of the page).
- `scrollYProgress` is a reactive value that updates as you scroll.

---

#### **2. `useSpring(scrollYProgress)`**

``` tsx 
const scaleX = useSpring(scrollYProgress);
```

- Converts the `scrollYProgress` value into a **spring animation**, making transitions smoother.
- This is applied to `scaleX`, which animates the width of the progress bar.

---

#### **3. `useTransform(scrollYProgress, [0, 0.5, 1], ["red", "green", "yellow"])`**

``` tsx
const background = useTransform(scrollYProgress, [0, 0.5, 1], ["red", "green", "yellow"]);
```

- **Transforms `scrollYProgress` into a color transition:**
    - At `0%` scroll → **Red**
    - At `50%` scroll → **Green**
    - At `100%` scroll → **Yellow**
- This is used to dynamically **change the background color** of the progress bar.

---

#### **4. `<motion.div>` (Animating the Progress Bar)**

```tsx
<motion.div
  style={{
    background,
    position: "sticky",
    width: "100%",
    height: "20px",
    top: "0",
    scaleX: scaleX,
    transformOrigin: "left",
  }}
></motion.div>
```

- **`motion.div`** is an animated `<div>` from Framer Motion.
- `scaleX` scales the width of the bar **horizontally** based on scroll progress.
- `transformOrigin: "left"` ensures the animation starts from the left side.
- `position: "sticky"` keeps the progress bar **fixed at the top** while scrolling.

---

#### **5. Scrollable Content**

```tsx
<div
  style={{
    maxWidth: "700px",
    margin: "auto",
  }}
>
  <p>... Lorem ipsum content ...</p>
</div>
```

- Provides enough **scrollable content** to see the progress bar in action.

---

### **Final Thoughts**

✅ **What This Code Does:**

- Tracks scroll progress (`useScroll`).
- Animates the progress bar **width** (`useSpring`).
- Dynamically changes the **background color** based on scroll position (`useTransform`).
- Uses **Framer Motion** for smooth animations.

---

## **📌 Basic Usage**

```tsx
import { useScroll } from "framer-motion";

function ScrollTracker() {
  const { scrollY, scrollYProgress } = useScroll();

  console.log("Pixels scrolled:", scrollY.get());
  console.log("Scroll progress (0 to 1):", scrollYProgress.get());

  return null;
}
```

### **🛠️ What Does This Hook Return?**

When you call `useScroll()`, it returns an object with the following properties:

|**Property**|**Description**|
|---|---|
|`scrollY`|A reactive value that represents **the number of pixels** scrolled from the top of the page.|
|`scrollYProgress`|A reactive value between `0` (top of page) and `1` (bottom of page), representing **the scroll progress percentage**.|

---

## **📌 Example: Using `scrollY` to Show Scroll Position**

Let's display the **exact scroll position** on the screen:

```tsx
import { useScroll } from "framer-motion";

function ScrollIndicator() {
  const { scrollY } = useScroll();

  return (
    <div style={{ position: "fixed", top: "10px", left: "10px", background: "black", color: "white", padding: "5px" }}>
      Scrolled: {scrollY.get()}px
    </div>
  );
}

export default ScrollIndicator;
```

✅ This will show the **exact number of pixels** you've scrolled.

---

## **📌 Example: Animating a Progress Bar with `scrollYProgress`**

A more **practical** use case is creating a **scroll progress bar** that visually shows how much of the page you’ve scrolled.

```tsx
import { motion, useScroll, useSpring } from "framer-motion";

function ScrollProgressBar() {
  const { scrollYProgress } = useScroll();
  const scaleX = useSpring(scrollYProgress, { stiffness: 100, damping: 30 });

  return (
    <motion.div
      style={{
        position: "fixed",
        top: 0,
        left: 0,
        width: "100%",
        height: "5px",
        background: "blue",
        scaleX: scaleX, // Animates the width
        transformOrigin: "left",
      }}
    />
  );
}

export default ScrollProgressBar;
```

✅ **Explanation:**

- `scrollYProgress` gives a **value between `0` and `1`** as you scroll.
- `useSpring(scrollYProgress)` makes the animation smooth.
- The `<motion.div>` scales horizontally based on scroll progress.

---

## **📌 Example: Changing Text Opacity Based on Scroll**

Another great use case is **dynamically changing styles** based on scroll position. Let's make some text fade in as you scroll:

```tsx
import { motion, useScroll, useTransform } from "framer-motion";

function ScrollFadeText() {
  const { scrollYProgress } = useScroll();

  // Change opacity from 0 to 1 as the user scrolls
  const opacity = useTransform(scrollYProgress, [0, 0.5, 1], [0, 0.5, 1]);

  return (
    <motion.h1 style={{ opacity, textAlign: "center", marginTop: "100vh" }}>
      Scroll Down to See Me Fade In!
    </motion.h1>
  );
}

export default ScrollFadeText;
```

✅ **How It Works:**

- The text **starts invisible** at the top (`opacity = 0`).
- As you scroll **halfway**, the text becomes **partially visible (`opacity = 0.5`)**.
- When you reach the bottom, the text is **fully visible (`opacity = 1`)**.

---

## **📌 Controlling `useScroll()` With a Specific Element**

By default, `useScroll()` tracks **the entire page's scroll position**, but you can track scrolling **inside a specific element** by passing a `ref`:

```tsx
import { useRef } from "react";
import { motion, useScroll } from "framer-motion";

function ScrollInsideDiv() {
  const containerRef = useRef(null);
  const { scrollYProgress } = useScroll({ container: containerRef });

  return (
    <div
      ref={containerRef}
      style={{ overflowY: "scroll", height: "300px", border: "1px solid black" }}
    >
      <motion.div
        style={{ height: "800px", background: "lightblue", scaleX: scrollYProgress }}
      />
    </div>
  );
}

export default ScrollInsideDiv;
```


✅ **Key Differences:**

- Instead of tracking **window scroll**, this tracks **scroll inside a specific div**.
- We pass `container: containerRef` to `useScroll()`.

---

## **📌 Summary of `useScroll()`**

|Feature|Description|
|---|---|
|`scrollY`|Tracks exact pixels scrolled.|
|`scrollYProgress`|Tracks scroll **progress (0 to 1)**.|
|Works with `useTransform`|Can be used to animate properties (e.g., opacity, color).|
|Can track a **specific element**|By passing `{ container: ref }`.|

---

### **💡 When to Use `useScroll()`**

🚀 Use `useScroll()` in Framer Motion when you want to:

- **Track how far a user has scrolled** (e.g., for analytics or UI changes).
- **Animate elements dynamically** based on scroll position.
- **Create a progress bar** that fills as the user scrolls.
- **Fade in/out elements** based on scroll position.
- **Change colors, sizes, or animations** smoothly as the page scrolls.



### **🛠 Understanding `{ stiffness: 200, damping: 330 }` in Framer Motion's `useSpring`**

In **Framer Motion**, `useSpring()` is used to create **smooth animations** with **realistic physics-based motion**. The `{ stiffness, damping }` values control **how the animation behaves**—whether it moves fast, slow, bouncy, or smooth.

---

## **📌 What Do `stiffness` and `damping` Do?**

|**Property**|**Effect**|
|---|---|
|**`stiffness`**|Controls how fast the animation **accelerates** toward the target value (higher = faster & snappier).|
|**`damping`**|Controls **resistance**—higher values slow down movement and reduce bouncing.|

---

## **📌 Example: `stiffness: 200, damping: 330`**

```tsx
import { motion, useScroll, useSpring } from "framer-motion";

function ScrollProgressBar() {
  const { scrollYProgress } = useScroll();

  const scaleX = useSpring(scrollYProgress, { stiffness: 200, damping: 330 });

  return (
    <motion.div
      style={{
        position: "fixed",
        top: 0,
        left: 0,
        width: "100%",
        height: "5px",
        background: "blue",
        scaleX: scaleX, // Smooth progress bar animation
        transformOrigin: "left",
      }}
    />
  );
}

export default ScrollProgressBar;

```


### **🔍 Explanation of `{ stiffness: 200, damping: 330 }`**

1. **`stiffness: 200`**
    
    - The animation **quickly accelerates** toward its target.
    - Higher stiffness makes it move **snappier**.
    - Lower values would make it **sluggish**.
2. **`damping: 330`**
    
    - High damping means the animation **stops smoothly** without bouncing.
    - If damping were low (`<30`), the animation would **overshoot** and **bounce**.

🚀 **Effect:**

- The progress bar **moves quickly** but **stops smoothly** without overshooting.

---

## **📌 Visualizing Different Values**

|`stiffness`|`damping`|**Effect**|
|---|---|---|
|`50`|`10`|Very slow & bouncy animation.|
|`100`|`50`|Smooth movement, slightly elastic.|
|`200`|`330`|Fast & smooth with **no bounce**.|
|`500`|`50`|**Very fast** but bouncy.|

---

### **🎯 When to Use Different Values**

- **For snappy UI animations (buttons, scroll bars, etc.)** → `{ stiffness: 200, damping: 330 }`
- **For bouncy, playful animations** → `{ stiffness: 150, damping: 20 }`
- **For slow, fluid animations (modals, loaders, etc.)** → `{ stiffness: 50, damping: 10 }`