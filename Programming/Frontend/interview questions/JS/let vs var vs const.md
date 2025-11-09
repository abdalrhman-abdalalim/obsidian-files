### 1️⃣ **Scope Differences**

- **`var` is function-scoped**:
    
    - It ignores block scope and is only confined within a function.
    - Example:
        
        `if (true) {   var x = 10; } console.log(x); // ✅ 10 (Accessible outside the block)`
        
- **`let` and `const` are block-scoped**:
    
    - They exist **only inside the block `{}` where they are declared**.
    - Example:
        
        `if (true) {   let y = 20;   const z = 30; } console.log(y); // ❌ ReferenceError console.log(z); // ❌ ReferenceError`
        

---

### 2️⃣ **Hoisting & Temporal Dead Zone (TDZ)**

- **`var` is hoisted with `undefined`**:
    
    `console.log(a); // ✅ undefined var a = 5;`
    
- **`let` and `const` are hoisted but not initialized (TDZ applies)**:
    
    `console.log(b); // ❌ ReferenceError let b = 10;`
    

---

### 3️⃣ **Re-declaration & Re-assignment**

|Case|`var`|`let`|`const`|
|---|---|---|---|
|**Re-declaration in the same scope?**|✅ Allowed|❌ Not allowed|❌ Not allowed|
|**Re-assignment?**|✅ Allowed|✅ Allowed|❌ Not allowed|

```js
var x = 5;
var x = 10; // ✅ No error

let y = 5;
let y = 10; // ❌ SyntaxError: Identifier 'y' has already been declared

const z = 5;
z = 10; // ❌ TypeError: Assignment to constant variable
```

---

### 4️⃣ **Use Cases**

|Use Case|Best Choice|
|---|---|
|Need **global variables** (not recommended)|`var` (but avoid using it)|
|Need **block-scoped variables** that can change|`let`|
|Need **constants** (values that won’t change)|`const`|

---

## 🏆 **Best Practices**

1. **Use `const` by default**:
    
    - If you don’t need to reassign a variable, use `const` for safety.
2. **Use `let` only when reassignment is needed**:
    
    - For variables that will change over time, like counters or state updates.
3. **Avoid `var`**:
    
    - It can introduce unexpected bugs due to hoisting and function-scoping.

---

## 🔥 **Quick Example to Show All Differences**

```js
function example() {
  if (true) {
    var a = 10;
    let b = 20;
    const c = 30;
  }
  
  console.log(a); // ✅ Works (var is function-scoped)
  console.log(b); // ❌ ReferenceError (let is block-scoped)
  console.log(c); // ❌ ReferenceError (const is block-scoped)
}

example();
```

---

- ❌ **Avoid `var`** (function-scoped, hoisting issues).
- ✅ **Use `let`** if you need to reassign values.
- ✅ **Use `const`** for constants (preferable by default).