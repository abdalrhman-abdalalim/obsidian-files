# 🔥 **JavaScript Callbacks** 🔥

## 📌 **What is a Callback Function?**

A **callback** is a function passed as an argument to another function and executed **later**. This is commonly used for **asynchronous operations** like API calls, file reading, and event handling.

---

## 📌 **Example of a Callback**

```js
function greet(name, callback) {
  console.log("Hello, " + name);
  callback();
}

function sayGoodbye() {
  console.log("Goodbye!");
}

greet("Ali", sayGoodbye);
```

✅ **Output:**

`Hello, Ali Goodbye!`

- `sayGoodbye` is **passed** as a callback and executed inside `greet()`.

---

## 📌 **Callback in Asynchronous JavaScript**

### ✅ **Example: Using `setTimeout()`**

```js
console.log("Start");

setTimeout(() => {
  console.log("This runs after 2 seconds");
}, 2000);

console.log("End");
```

✅ **Output:**

`Start -> End ->  This runs after 2 seconds`

- The function inside `setTimeout()` is a **callback** that runs after a delay.

---

## 📌 **Callbacks in Event Listeners**

```js
document.getElementById("btn").addEventListener("click", function () {
  console.log("Button Clicked!");
});
```

- The function inside `addEventListener()` is a **callback** executed when the button is clicked.

---

## 📌 **Callbacks with Asynchronous Operations**

### ✅ **Example: Simulating an API Call**

```js
function fetchData(callback) {
  setTimeout(() => {
    console.log("✅ Data fetched!");
    callback();
  }, 3000);
}

function processData() {
  console.log("📊 Processing Data...");
}

fetchData(processData);
```

✅ **Output:**


`✅ Data fetched! -> 📊 Processing Data...`

- `processData` is a callback that runs **after** `fetchData` completes.

---

## 📌 **Callback Hell (Pyramid of Doom)**

Too many nested callbacks make the code **hard to read and debug**.

```js
function step1(callback) {
  setTimeout(() => {
    console.log("Step 1 complete");
    callback();
  }, 1000);
}

function step2(callback) {
  setTimeout(() => {
    console.log("Step 2 complete");
    callback();
  }, 1000);
}

function step3(callback) {
  setTimeout(() => {
    console.log("Step 3 complete");
    callback();
  }, 1000);
}

// Callback Hell 😭
step1(() => {
  step2(() => {
    step3(() => {
      console.log("All steps completed!");
    });
  });
});
```


✅ **Fix: Use Promises instead of Callbacks!**

```js
function step1() {
  return new Promise((resolve) => {
    setTimeout(() => {
      console.log("Step 1 complete");
      resolve();
    }, 1000);
  });
}

function step2() {
  return new Promise((resolve) => {
    setTimeout(() => {
      console.log("Step 2 complete");
      resolve();
    }, 1000);
  });
}

function step3() {
  return new Promise((resolve) => {
    setTimeout(() => {
      console.log("Step 3 complete");
      resolve();
    }, 1000);
  });
}

// Promise Chain (Cleaner Code)
step1()
  .then(step2)
  .then(step3)
  .then(() => console.log("All steps completed!"));
```

✅ **Output (Same result, but cleaner code!)**

---

## 📌 **Summary**

|Feature|Explanation|
|---|---|
|**Definition**|A function passed as an argument and executed later.|
|**Common Uses**|Async operations (API calls, timers, event listeners).|
|**Issue**|Callback Hell (Too many nested functions).|
|**Better Alternative**|Use **Promises** or **async/await**.|

🔥 **Rule of Thumb:**  
Callbacks are useful, but for complex async logic, use **Promises or async/await** for cleaner code! 🚀
