Hoisting is JavaScript's default behavior of moving declarations to the top

---

Variables defined with `let` and `const` are hoisted to the top of the block, but not _initialized_.

Meaning: The block of code is aware of the variable, but it cannot be used until it has been declared.

Using a `let` variable before it is declared will result in a `ReferenceError`.
Using a `const` variable before it is declared, is a syntax error, so the code will simply not run.

---
JavaScript only hoists declarations, not initializations.

```js
var x = 5;  // Initialize x
y=7;

elem = document.getElementById("demo");      // Find an element 
elem.innerHTML = "x is " + x + " and y is " + y;  // Display x and y

var y = 7;  // Initialize y
```

### 🔹 Key Points About Hoisting:

1. **Declarations are Hoisted, Not Initializations**
    
    - JavaScript moves **variable and function declarations** to the top of their scope before execution.
    - However, **initializations (assignments)** remain in place.
2. **`var` is Hoisted with `undefined`**
    
    - Variables declared with `var` are hoisted **with a default value of `undefined`**.
    - Example:
        
        `console.log(a); // undefined (Declaration is hoisted, but initialization is not) var a = 10;`
        
3. **`let` and `const` are Hoisted but in the Temporal Dead Zone (TDZ)**
    
    - They **do not get initialized** like `var` does.
    - Accessing them before declaration results in a **ReferenceError**.
    - Example:
        
        `console.log(b); // ReferenceError: Cannot access 'b' before initialization let b = 20;`
        
4. **Functions are Fully Hoisted**
    
    - Function **declarations** are hoisted **with their full definition**.
    - Example:
        
        `greet(); // Works fine function greet() {   console.log("Hello!"); }`
        
    - But function **expressions** (assigned to `var`, `let`, or `const`) are **not hoisted** the same way:
        
        `hello(); // TypeError: hello is not a function var hello = function () {   console.log("Hi!"); };`
        

---


### 🔥 Quick Summary:

|Feature|`var`|`let`|`const`|
|---|---|---|---|
|Hoisted?|✅ Yes (initialized as `undefined`)|✅ Yes (but not initialized)|✅ Yes (but not initialized)|
|TDZ (Temporal Dead Zone)?|❌ No|✅ Yes|✅ Yes|
|Reassignable?|✅ Yes|✅ Yes|❌ No (must be assigned at declaration)|
|Scope|Function|Block|Block|

Would you like a **visualization** of hoisting behavior? 🚀
