### **📝 Using `dangerouslySetInnerHTML` for Line Breaks**

If you want to **replace periods (`.`) with line breaks (`<br>`)** to display instructions **line by line**, you can do it like this:

#### **✅ Correct Approach:**

```tsx
export default function MealInstructions({ meal }: { meal: Meal }) {
  return (
    <div
      dangerouslySetInnerHTML={{
        __html: meal.instructions.replace(/(?<=[A-Za-z])\./g, "<br>"),
      }}
    />
  );
}
```

### **🛑 Important Considerations**

1. **Security Risk ⚠️**
    
    - If `meal.instructions` comes from user input or an external source, it could contain **malicious scripts**.
    - To **sanitize** it, use libraries like [DOMPurify](https://www.npmjs.com/package/dompurify).
2. **Alternative: Use `.split(".")` for safer rendering**  
    Instead of `dangerouslySetInnerHTML`, you can **split** instructions into an array and render them safely:
    
    ```tsx
    export default function MealInstructions({ meal }: { meal: Meal }) {
  return (
    <div>
      {meal.instructions.split(".").map((line, index) =>
        line.trim() ? <p key={index}>{line}.</p> : null
      )}
    </div>
  );
}
```
    
    ✅ **Why is this better?**
    
    - It avoids **XSS vulnerabilities**.
    - Uses **React's safe JSX rendering**.