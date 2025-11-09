## ✅ Why Use Cypress?

Cypress is an **all-in-one testing framework** built specifically for modern web applications. It simplifies and strengthens testing with:

- ✅ **E2E (End-to-End) & Component Testing** – real-world testing like a user
    
- ✅ **Built-in Assertion Library** – no need for external tools like Chai or Mocha
    
- ✅ **Mocking & Stubbing** – intercept and control network requests easily
    
- ✅ **Runs in the Browser** – gives native access to the DOM and app internals
    
- ✅ **JavaScript/TypeScript Friendly** – use your normal web dev language
    
- ✅ **CI/CD Integration** – easily runs in pipelines
    
- ✅ **Great Developer Experience** – interactive test runner UI
    
- ✅ **Generally Not Flaky** – if you follow Cypress best practices
    

---

## 🚀 Installation

`npm install cypress --save-dev npx cypress open`

> ✅ **Note**: Make sure your dev server is running when you open Cypress.

---

## 🧠 Core Cypress Fundamentals

### 1. `describe()` Block

This wraps a group of related tests.


`describe('Login Page', () => {   // test cases go here });`

- First argument: test suite description
    
- Second argument: callback with the tests
    

---

### 2. `it()` Block

This defines an individual test case.

`it('should log in successfully', () => {   // individual test logic here });`

---

### 3. `cy` Object

Cypress provides the `cy` object for commands (like `cy.visit()`, `cy.get()`, etc).

#### Examples:

```tsx
cy.visit('/'); // go to homepage
cy.get('[data-test="submit-btn"]').click(); // click a button
cy.get('input[name="email"]').type('user@example.com');
cy.get('h1').should('contain.text', 'Welcome');

```


---

## ⚠️ Important Notes

### 🔁 Cypress Is Async

- Cypress commands are **chained**, not returned like in `Promise` or `async/await`.
    
- You can **chain `.then()`** to work with results:
    

`cy.get('h1').then(($el) => {   // $el is the resolved DOM element });`

> 🔹 `.then()` is Cypress-specific — **not** a regular Promise `.then()`  
> 🔹 Cypress commands yield values like `cy.get()` yielding a DOM element

---

### 🧪 Assertions

After selecting an element, chain an assertion:

`cy.get('h1').should('contain.text', 'Dashboard');`

---

### 🏷️ Best Practice: Use `data-test` Attributes

Use selectors that don’t depend on fragile structure or styling:

`<h1 data-test="header-title">Examples</h1>`

`cy.get('[data-test="header-title"]').should('contain.text', 'Examples');`