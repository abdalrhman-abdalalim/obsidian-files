**Pure Function:** A function that has no side effects and always returns the same output for the same inputs.

### **Key Benefits:**

- Makes code easier to understand and use.
- Encapsulates a small, well-defined piece of logic.

### **Downsides:**

- Cannot modify or affect anything outside its scope.

### **Best Practice:**

It's recommended to write pure functions whenever possible. However, if a function needs to interact with external systems (e.g., API calls, database operations), making it a purely functional approach may not always be feasible.

---

### **Impure Function Example**

```js
let array = [1, 2, 3];  let addToArray = (ele) => {     array.push(ele);  };

``` 

#### **Why is this impure?**

1. **Side Effect**: It modifies the global `array` variable directly.
2. **Inconsistent Output**: If you call `addToArray(4)` multiple times, `array` keeps changing.
    - Example:
	    ```js
		addToArray(4);  console.log(array); // [1, 2, 3, 4] addToArray(4);  
		 console.log(array); // [1, 2, 3, 4, 4]
```
        
    - The function does not return a value but changes the existing array.

---

### **Pure Function Example**

```js
let addToArray = (ar, ele) => {     return [...ar, ele]; };
```
#### **Why is this pure?**

1. **No Side Effects**: It does **not** modify the original array. Instead, it returns a **new array**.
2. **Consistent Output**:
    - Given the same input, it always returns the same output.
    - Example:
        ```js
          let result1 = addToArray(array, 4); 
        console.log(result1); // [1, 2, 3, 4]  
        let result2 = addToArray(array, 4); 
        console.log(result2); // [1, 2, 3, 4]
```
        
    - The function does **not** change `array`, ensuring immutability.

---

### **Conclusion**

- **Impure functions** modify existing data, making debugging harder and leading to unexpected behavior.
- **Pure functions** return new values without modifying the original ones, making them predictable and easier to test.
- **Best Practice:** Prefer writing pure functions unless mutation is necessary (e.g., interacting with APIs