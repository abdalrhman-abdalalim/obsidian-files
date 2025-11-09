### 🔹 **Gradient Border for Buttons**

`button {   width: 400px;   border-image: linear-gradient(to right, blue, red) 1 1 1 1; }`

- Uses **`border-image`** to create a gradient border.
- The `linear-gradient(to right, blue, red)` applies a **blue-to-red** gradient.
- `1 1 1 1` defines the **border slice** (how the border image is divided).

✅ **Better Alternative:** If `border-image` doesn't work well in some browsers, you can use `background-clip`:

```css
button {
  width: 400px;
  padding: 10px;
  border: 5px solid transparent;
  background: linear-gradient(white, white) padding-box,
              linear-gradient(to right, blue, red) border-box;
}
```

---

### 🔹 **Responsive Multi-Column Layout**

```css
div {
  width: min(1000px, 100%); /* Responsive width */
  margin: 0 auto;
  columns: 3 300px;
  column-gap: 1em;
}
```


- `width: min(1000px, 100%)` → Makes sure the div doesn't exceed `1000px` but remains **responsive**.
- `columns: 3 300px;` → Attempts to create **3 columns** with a minimum **width of 300px per column**.
- `column-gap: 1em;` → Defines the **space between columns**.

✅ **Alternative for better control:**

```css
display: grid;
grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
```

- **More control over responsive behavior** than `columns`.

---

### 🔹 **Making Images Responsive Inside the Columns**

`img {   display: block;   margin-bottom: 1em;   width: 100%; }`

- `display: block;` → Removes inline spacing issues.
- `margin-bottom: 1em;` → Adds spacing between images.
- `width: 100%;` → Makes images fit their parent column width.

✅ **Alternative: Add `object-fit` for better scaling**

`img {   width: 100%;   height: auto;   object-fit: cover; }`

---

### 🔹 **Customizing Input Appearance**

`input, input:focus {   accent-color: red;   caret-color: red; }`

- `accent-color: red;` → Changes the **checkbox, radio button, and progress bar color**.
- `caret-color: red;` → Changes the **cursor color** in text inputs.

---

### 🔹 **Positioning Using `inset`**


`position: absolute; inset: 100px 10px 5px 7px;`

- `inset` is shorthand for:
    
    `top: 100px; right: 10px; bottom: 5px; left: 7px;`
    

✅ **To Center an Absolute Child:**

```css
.parent {
  position: relative;
}
.child {
  position: absolute;
  inset: 0;
  margin: auto;
}

```

- This **centers** the element inside `.parent`.

---

### 🔹 **Scrolling & Shadows**


`overflow-y: auto; filter: drop-shadow(5px 5px 5px black);`

- `overflow-y: auto;` → Enables **vertical scrolling** when content exceeds the container height.
- `drop-shadow(5px 5px 5px black);` → Adds a **shadow effect** with **(x, y, blur, color)**.

---

### 🔹 **Animating Height Without Fixed Sizes**

`grid-template-rows: 1.5em 0fr;`

**Before Opening:**

`grid-template-rows: 1.5em 0fr;`

**After Opening:**

`grid-template-rows: 1.5em 1fr;`

- This allows smooth **height animations** for elements with **dynamic content**.

---

### 🔹 **Custom `content` for Each Element**


`content: attr(data-label);`

- **Dynamically sets content** based on an element's **data-label attribute**.
- Example:
	
    `<span data-label="User">👤</span>`
    
    `span::before {   content: attr(data-label) ": ";   font-weight: bold; }`
    
    ✅ **Output:**  
    `User: 👤`

---

### 🔹 **Scrollable Paragraph Example**

`p {   width: 200px;   height: 200px;   background-color: red;   overflow-y: auto; }`

- Creates a **fixed-size box** with **scrolling enabled** if the content overflows.

---


### 🔹 **animated border effect**
This code creates an **animated border effect** around a button using **CSS Custom Properties (`@property`)**, `conic-gradient()`, and keyframe animations. Let’s break it down step by step.
## **1️⃣ `@property --angle`**

```css
@property --angle {
  syntax: "<angle>";
  initial-value: 0deg;
  inherits: false;
}
```

- `@property` allows defining **CSS Custom Properties** (`--angle`) that can be animated.
- `syntax: "<angle>";` → Defines `--angle` as an **angle value** (e.g., `0deg`, `90deg`).
- `initial-value: 0deg;` → The default starting value of `--angle` is **0 degrees**.
- `inherits: false;` → The property **does not inherit** its value from parent elements.

---

## **2️⃣ Styling the Button**

`button {   position: absolute;   inset: 0;   margin: auto;   width: 400px;   height: 100px;   background: white;   border: none;   position: relative; }`

- `position: absolute;` → Centers the button **inside its parent** using `inset: 0; margin: auto;`.
- `width: 400px; height: 100px;` → Defines the button size.
- `background: white;` → Sets the **button background color**.
- `border: none;` → Removes any default button border.
- `position: relative;` → Ensures the `::before` pseudo-element is **positioned relative** to the button.

---

## **3️⃣ Creating the Animated Border**

`button::before {   content: "";   position: absolute;   inset: -5px; /* Controls border thickness */   border-radius: inherit;   z-index: -1;   background: conic-gradient(from var(--angle), blue, red, blue);   animation: spin-border 1s infinite; }`

- `::before` creates a **pseudo-element** behind the button.
- `content: "";` → Makes sure the `::before` element is **rendered**.
- `position: absolute; inset: -5px;` → Expands the pseudo-element **slightly larger** than the button (creating a border effect).
- `border-radius: inherit;` → Inherits the button's border radius (for rounded buttons).
- `z-index: -1;` → Moves the pseudo-element **behind the button**.
- `background: conic-gradient(from var(--angle), blue, red, blue);`
    - `conic-gradient()` creates a **rotating gradient effect**.
    - `from var(--angle);` makes the gradient **rotate dynamically**.
- `animation: spin-border 1s infinite;` → Starts the animation.

---

## **4️⃣ Animating the Border**

`@keyframes spin-border {   from {     --angle: 0deg;   }   to {     --angle: 360deg;   } }`

- Defines a keyframe animation **`spin-border`**.
- `from { --angle: 0deg; }` → Starts at `0 degrees`.
- `to { --angle: 360deg; }` → Rotates the gradient **fully around**.
- Since `@property --angle` allows animations, **the gradient smoothly rotates**.
## **🔹 scroll-snap-type: y mandatory
- **Purpose:**  
    Enables scroll snapping along the vertical (y) axis for the entire document.
    
- **Axis (`y`):**  
    Setting it to `y` indicates that the scroll snapping behavior will apply to vertical scrolling. If you were working with horizontal scrolling, you might use `x` instead.
    
- **Snapping Behavior (`mandatory`):**  
    The `mandatory` value means the browser must force snapping at the designated snap points. When scrolling, once the user releases their scroll gesture, the viewport will automatically "snap" to the closest snap point defined on the child elements.
    
- **How It Works:**  
    For the snap behavior to take effect, you should have child elements within a scroll container (or within the document, in this case) that specify their snap alignment using properties like `scroll-snap-align` (e.g., `scroll-snap-align: center;`). In our example, you might have sections within your HTML document defined with such a property, which tells the browser where to "snap" when scrolling vertically.

## **🔹 scroll-behavior: smooth
- **Purpose:**  
    Enables smooth scrolling animations for user interactions like clicking on anchor links or programmatically triggered scrolls.
    
- **Smooth Scrolling:**  
    Rather than jumping instantly from one part of the page to another, smooth scrolling animates the transition. This creates a more pleasant and controlled user experience when navigating through content.
    
- **Usage Scenario:**  
    For example, if you have links that navigate to different sections (e.g., `<a href="#section1">Go to Section 1</a>`), clicking such a link will scroll smoothly to the target element instead of jumping abruptly.
## **🔹 scroll-snap-align: start
- **Defining the Snap Position:**  
    `scroll-snap-align` indicates how an element should align itself within the scroll container when a scroll snap is triggered.
    
    - **`start` Value:**  
        With the value `start`, the element will be positioned so that its starting edge (top for vertical scrolling or left for horizontal scrolling) aligns with the snap position defined by its container. This means that when scrolling stops, the beginning of your element lines up perfectly with the beginning of the container's visible area.
