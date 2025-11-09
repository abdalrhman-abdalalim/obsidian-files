## 🔁 What Is the Event Loop?

JavaScript is **single-threaded**, meaning it runs **one thing at a time** on the **main thread**.

But we often need to perform **asynchronous** operations—like fetching data, setting timers, or listening for clicks—**without blocking** the rest of the app.

This is where the **event loop** comes in: it manages these tasks and decides **when** to run them.

---

## 🧠 Key Concepts to Understand

### 1. **Call Stack**

- Where your **functions** are executed.
    
- Follows a **Last-In, First-Out (LIFO)** rule.
    
- If it’s busy, nothing else can run.
    

### 2. **Web APIs**

- These are **browser-provided** or Node.js tools that handle async work like `setTimeout`, `fetch`, or event listeners.
    

### 3. **Callback Queue (Macrotask Queue)**

- Stores callbacks from things like `setTimeout`, `setInterval`, DOM events, etc.
    
- Runs **after** the microtask queue is empty.
    

### 4. **Microtask Queue**

- Stores **Promises**, `queueMicrotask()`, and `MutationObserver` callbacks.
    
- Has **higher priority** than the callback queue.
    

### 5. **Event Loop**

- Keeps checking:
    
    - Is the call stack empty?
        
    - Any microtasks to run?
        
    - Any tasks in the callback queue?
        
- Executes them **in order of priority**.

---

## 📜 Example: Order of Execution

```js
console.log("Start");

setTimeout(() => {
    console.log("setTimeout Callback");
}, 0);

Promise.resolve().then(() => {
    console.log("Promise Resolved");
});

console.log("End");
```

## ✅ Output:

```js
Start
End
Promise Resolved
setTimeout Callback
```

### Why?

- `console.log("Start")` runs immediately.
    
- `setTimeout(..., 0)` is sent to Web API → then callback queue.
    
- `Promise.resolve().then(...)` goes to **microtask queue**.
    
- `console.log("End")` runs next.
    
- Event loop checks: Microtask queue has a Promise → it runs first.
    
- Then, it runs `setTimeout` from the callback queue.

![[Event-Loop-in-JavaScript.jpg]]