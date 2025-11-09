### **📌 `viewport={{ once: true }}` in Framer Motion**

In **Framer Motion**, the `viewport` prop is used to control how elements animate when they enter the viewport (i.e., when they appear on the screen).

#### **💡 What does `once: true` do?**

`viewport={{ once: true }}` means **the animation will only run once when the element enters the viewport**.

🔹 **Without `once: true`** → The animation will re-trigger **every time** the user scrolls the element in and out of view.  
🔹 **With `once: true`** → The animation runs **only the first time** the element appears on the screen and does not replay.