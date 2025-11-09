In JavaScript, the `sort()` method sorts arrays **in place** (mutating the original array). By default, it sorts elements as **strings**, which can lead to unexpected results with numbers.

### **Problem with Default `sort()` for Numbers**

const numbers = [10, 5, 100, 2, 1000];
numbers.sort();
console.log(numbers); // [10, 100, 1000, 2, 5] (WRONG!)

**Why?**

- JS converts numbers to strings and compares them lexicographically (like dictionary order).
    

---

### **Solution: Pass a Compare Function**

To sort numbers correctly, pass a **compare function** to `sort()`:


const numbers = [10, 5, 100, 2, 1000];
numbers.sort((a, b) => a - b);
console.log(numbers); // [2, 5, 10, 100, 1000] (CORRECT!)

### **How the Compare Function Works**

- **`(a, b) => a - b`** → Sorts in **ascending** order (smaller to bigger).
    
- **`(a, b) => b - a`** → Sorts in **descending** order (bigger to smaller).
    

|Return Value|Sorting Order|
|---|---|
|**`a - b`**|`a` comes before `b` (ascending)|
|**`b - a`**|`b` comes before `a` (descending)|