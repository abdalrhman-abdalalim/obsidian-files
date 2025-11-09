## JavaScript Interview Questions

- **1. What is the difference between var, let, and const in JavaScript?**
    - `var`: Function-scoped, hoisted, can be redeclared.  
    - `let`: Block-scoped, not hoisted the same way, can be reassigned but not redeclared in the same scope.  
    - `const`: Block-scoped, cannot be reassigned or redeclared (value is constant reference).

---

- **2. Explain the concept of closures in JavaScript with an example.**
    - A closure is when a function "remembers" variables from its outer scope, even after the outer function has finished executing.  
    ```js
    function outer() {
      let count = 0;
      return function inner() {
        count++;
        return count;
      };
    }
    const counter = outer();
    counter(); // 1
    counter(); // 2
    ```

---

- **3. How does the `this` keyword work in JavaScript?**
    - Depends on context:  
        - In global scope → refers to `window` (in browsers).  
        - Inside a method → refers to the object calling the method.  
        - In arrow functions → inherits `this` from its enclosing scope.  
        - In event handlers → refers to the element receiving the event.  

---

- **4. What are higher-order functions, and can you provide an example?**
    - A higher-order function is one that takes a function as an argument or returns a function.  
    ```js
    const numbers = [1, 2, 3];
    const doubled = numbers.map(num => num * 2); // map is HOF
    ```

---

- **5. What is the difference between synchronous and asynchronous JavaScript?**
    - **Synchronous**: Code runs line by line, blocking further execution until current task completes.  
    - **Asynchronous**: Allows non-blocking operations (e.g., `setTimeout`, Promises, async/await).  

---

- **6. Explain the difference between forEach and map methods in arrays.**
    - `forEach`: Executes a function for each element, returns `undefined`.  
    - `map`: Executes a function for each element, returns a **new array** with transformed values.  

---

- **7. What is the purpose of promises, and how do you use them?**
    - Promises represent the eventual completion (or failure) of an asynchronous operation.  
    ```js
    fetch("/data.json")
      .then(response => response.json())
      .then(data => console.log(data))
      .catch(error => console.error(error));
    ```

---

- **8. What are arrow functions, and how do they differ from regular functions?**
    - Shorter syntax for functions.  
    - Do **not** have their own `this` (lexically bind `this`).  
    - Cannot be used as constructors.  
    ```js
    const add = (a, b) => a + b;
    ```

---

- **9. How does event delegation work in JavaScript?**
    - Instead of adding event listeners to many child elements, add one listener to their parent.  
    - The event bubbles up, and you can check `event.target` to handle specific children.  
    ```js
    document.getElementById("list").addEventListener("click", e => {
      if (e.target.tagName === "LI") {
        console.log("Clicked", e.target.textContent);
      }
    });
    ```

---

- **10. What are REST APIs?**
    - REST (Representational State Transfer) is an architectural style for building APIs that use HTTP methods (GET, POST, PUT, DELETE) to interact with resources.  

---

- **11. How do you ensure the security of an API?**
    - Use authentication & authorization (JWT, OAuth).  
    - Validate & sanitize inputs.  
    - Use HTTPS.  
    - Rate limiting & throttling.  
    - Keep sensitive data out of URLs.  

---

- **12. Explain the purpose of HTTP status codes in API responses.**
    - They indicate the result of an HTTP request:  
        - `200 OK` → Success  
        - `201 Created` → Resource created  
        - `400 Bad Request` → Client error  
        - `401 Unauthorized` → Authentication required  
        - `404 Not Found` → Resource doesn’t exist  
        - `500 Internal Server Error` → Server-side error  

---

- **13. How would you optimize API performance?**
    - Caching (server-side & client-side).  
    - Pagination & limiting results.  
    - Use efficient data formats (e.g., JSON over XML).  
    - Load balancing & CDN.  
    - Database indexing & query optimization.  

---

- **14. What is the difference between GET and POST methods in REST APIs?**
    - `GET`: Retrieve data, should be idempotent (no side effects). Parameters usually in URL query string.  
    - `POST`: Send data to create/update resources. Parameters usually in request body.  

---

- **15. What is the difference between `null` and `undefined`?**
    - `undefined`: A variable has been declared but has not been assigned a value.  
    - `null`: An explicit assignment that represents "no value" or "empty".  
    ```js
    let a;        // undefined
    let b = null; // null
    ```

---

- **16. How does the Event Loop work in the browser?**
    - JavaScript is single-threaded and uses the Event Loop to handle asynchronous operations.  
    - Process:  
        1. **Call Stack** executes synchronous code.  
        2. **Web APIs** (like `setTimeout`, `fetch`) handle async tasks.  
        3. **Callback Queue / Microtask Queue** stores callbacks once tasks complete.  
        4. **Event Loop** pushes them to the call stack when it's empty.  
    ```js
    console.log("Start");

    setTimeout(() => console.log("Timeout"), 0);

    Promise.resolve().then(() => console.log("Promise"));

    console.log("End");
    // Output: Start → End → Promise → Timeout
    ```

---


