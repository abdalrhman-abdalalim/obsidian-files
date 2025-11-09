## 1. Difference between `em` and `rem` units in CSS
- **Toggle Explanation**
    - Both are relative units, but their reference point is different.
    - **`em`**: Relative to parent font-size (can compound).
    - **`rem`**: Relative to root font-size (predictable, consistent).
    - **In short**: Use `em` for local scaling, `rem` for global consistency.

---

## 2. Purpose of the meta viewport tag in responsive design
- **Toggle Explanation**
    - Without it → Page shrinks on mobile, content looks tiny.
    - With it → Page matches device width, scales properly.
    - Example:
        ```html
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        ```

---

## 3. Pseudo-elements in CSS
- **Toggle Explanation**
    - Special selectors to style specific parts of elements.
    - Examples:
        - `::before` → insert before content.
        - `::after` → insert after content.
        - `::first-line` → style first line.
        - `::first-letter` → style first letter.
        - `::selection` → style selected text.

---

## 4. Difference between inline, inline-block, and block elements
- **Toggle Explanation**
    - **Block**: Full width, new line, can set width/height.  
    - **Inline**: Flow with text, no width/height.  
    - **Inline-block**: Inline placement but block behavior inside (can set width/height).  

---

## 5. Difference between CSS positioning types
- **Toggle Explanation**
    - **static**: Default, no offsets.  
    - **relative**: Offset relative to itself.  
    - **absolute**: Relative to positioned ancestor or root.  
    - **fixed**: Relative to viewport, doesn’t move on scroll.  
    - **sticky**: Relative until threshold → then acts like fixed.  
