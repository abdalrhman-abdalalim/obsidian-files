### 🔥 **Statically Typed vs Dynamically Typed Languages**

Programming languages can be categorized based on **how they handle variable types**. The two main categories are **statically typed** and **dynamically typed** languages.

---

## 🆚 **Key Differences**

|Feature|Statically Typed|Dynamically Typed|
|---|---|---|
|**Type Checking**|At compile-time|At runtime|
|**Type Declaration**|Required explicitly|Inferred automatically|
|**Error Detection**|Before execution|During execution|
|**Flexibility**|Less flexible, but safer|More flexible, but riskier|
|**Performance**|Faster (optimized at compile time)|Slower (types resolved at runtime)|
|**Examples**|C, C++, Java, TypeScript|JavaScript, Python, Ruby|

---

## 📌 **1️⃣ Statically Typed Languages**

✅ **Variables have fixed types and must be declared before use.**  
✅ **Type errors are caught at compile-time**, preventing runtime crashes.  
❌ **Less flexibility**, but safer and faster execution.

### **Example: Java (Statically Typed)**

`int num = "hello"; // ❌ Compile-time error: Type mismatch`

- The above code will fail **before running** because `"hello"` is a string, not an `int`.

---

## 📌 **2️⃣ Dynamically Typed Languages**

✅ **Variables can hold any type, and types can change at runtime.**  
✅ **More flexible and easier to write.**  
❌ **Errors may occur at runtime**, leading to potential bugs.

### **Example: JavaScript (Dynamically Typed)**

`let num = 5;  num = "hello"; // ✅ No error! Type changed at runtime console.log(num); // Outputs: "hello"`

- This code runs **without errors** even though `num` was initially a number and later a string.

---

## 🚀 **Pros & Cons**

|Feature|Statically Typed|Dynamically Typed|
|---|---|---|
|✅ **Error Prevention**|Fewer runtime errors|More prone to runtime errors|
|✅ **Performance**|Faster execution (optimized at compile-time)|Slightly slower (type-checking at runtime)|
|✅ **Flexibility**|Less flexible (strict types)|More flexible (can change types)|
|✅ **Development Speed**|Slower (more code for types)|Faster (no need to specify types)|

---

## 🏆 **When to Use What?**

- **Use Statically Typed Languages** when:
    
    - You need **high performance** (e.g., game engines, system software).
    - The project is **large-scale** (stronger type safety reduces errors).
    - You want **better tooling & auto-completion** (TypeScript, Java).
- **Use Dynamically Typed Languages** when:
    
    - You need **rapid development** (prototyping, startups).
    - The project is **smaller & doesn't require strict type checking**.
    - You prefer **ease of coding & flexibility** (Python, JavaScript).

---

## 🔥 **Best of Both Worlds?**

**TypeScript** is a statically typed version of JavaScript!

- **JavaScript (dynamic)** → `let x = 10;`
- **TypeScript (static)** → `let x: number = 10;`

✅ Gives the flexibility of JavaScript while adding type safety!

---

|**Comparison**|**Statically Typed**|**Dynamically Typed**|
|---|---|---|
|**Type Checking**|Compile-time|Runtime|
|**Error Handling**|Fewer runtime errors|More runtime errors|
|**Flexibility**|Less flexible|More flexible|
|**Performance**|Faster|Slower|
|**Examples**|C, Java, TypeScript|Python, JavaScript, Ruby|

**🚀 Rule of Thumb:** Use statically typed languages for performance & safety, and dynamically typed languages for flexibility & speed!