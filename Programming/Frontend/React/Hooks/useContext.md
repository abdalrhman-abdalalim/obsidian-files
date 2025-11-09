# **🌟 `useContext` in React: A Complete Guide**

`useContext` is a React Hook that allows you to **consume values from a React Context** without needing to wrap components in a Consumer component.

It helps **avoid prop drilling** when passing data to deeply nested components.

---

## **📌 Syntax**

`const contextValue = useContext(MyContext);`

- `MyContext` is the **context object** created using `React.createContext()`.
- `contextValue` gives **access to the current value** of the context.

---

## **🛠️ Example 1: Basic Usage of `useContext`**

Let's create a **theme context** and use `useContext` to toggle between light and dark modes.

### **1️⃣ Create the Context**

`import { createContext } from "react";  export const ThemeContext = createContext("light"); // Default value: 'light'`

### **2️⃣ Provide Context at a Higher Level**

```tsx
import { useState } from "react";
import { AuthContext } from "./AuthContext";
import Login from "./Login";
import Profile from "./Profile";

export default function App() {
  const [user, setUser] = useState(null);

  return (
    <AuthContext.Provider value={{ user, setUser }}>
      <Login />
      <Profile />
    </AuthContext.Provider>
  );
}
```


- The **`ThemeContext.Provider`** provides the `theme` and `setTheme` values.
- Any **child component** can now access `theme` and `setTheme`.

### **3️⃣ Consume Context in a Child Component**

```tsx
import { useContext } from "react";
import { AuthContext } from "./AuthContext";

export default function Login() {
  const { setUser } = useContext(AuthContext);

  return <button onClick={() => setUser({ name: "Abdo" })}>Login</button>;
}
```

### **🔍 What’s Happening?**

✔ `useContext(ThemeContext)` allows `ThemeToggle` to access `theme` and `setTheme` **without prop drilling**.  
✔ Clicking the button **toggles** between **light** and **dark** themes.

---

## **🛠️ Example 2: Using `useContext` with Authentication**

A real-world example where `useContext` is useful is **authentication management**.

### **1️⃣ Create an Authentication Context**

`import { createContext } from "react";  export const AuthContext = createContext(null);`

### **2️⃣ Provide the Authentication Context**

```tsx
import { useState } from "react";
import { AuthContext } from "./AuthContext";
import Login from "./Login";
import Profile from "./Profile";

export default function App() {
  const [user, setUser] = useState(null);

  return (
    <AuthContext.Provider value={{ user, setUser }}>
      <Login />
      <Profile />
    </AuthContext.Provider>
  );
}
```

### **3️⃣ Consume the Context in a Login Component**

```tsx
import { useContext } from "react";
import { AuthContext } from "./AuthContext";

export default function Login() {
  const { setUser } = useContext(AuthContext);

  return <button onClick={() => setUser({ name: "Abdo" })}>Login</button>;
}
```

### **4️⃣ Consume the Context in a Profile Component**

```tsx
import { useContext } from "react";
import { AuthContext } from "./AuthContext";

export default function Profile() {
  const { user } = useContext(AuthContext);

  return <h2>{user ? `Welcome, ${user.name}!` : "Please log in"}</h2>;
}
```
### **🔍 What’s Happening?**

✔ When the user clicks **"Login"**, `setUser` updates the state.  
✔ `Profile` automatically receives the updated **user data**.  
✔ No need to pass `user` and `setUser` manually via props!

---

## **🚀 When to Use `useContext`?**

✅ **Use `useContext` when:**

- You need to **share state** across multiple deeply nested components.
- You're dealing with **global app state** like **authentication**, **theme**, or **language settings**.

❌ **Avoid `useContext` when:**

- Your state **changes frequently** (e.g., animations, form fields). **Use `useState` or `useReducer` instead**.
- You have **small components** that don’t need global state.

---

## **📌 Common Mistakes & Fixes**

### **❌ Forgetting the Context Provider**


`function Component() {   const theme = useContext(ThemeContext); // ❌ Error: No Provider found }`

✅ **Fix:** Wrap the component inside a `<ThemeContext.Provider>`.

`<ThemeContext.Provider value="dark">   <Component /> </ThemeContext.Provider>`

---

### **❌ Updating Context State Without `Provider`**


`const { user, setUser } = useContext(AuthContext);` 
`setUser({ name: "John" }); // ❌ Error if setUser is undefined`

✅ **Fix:** Ensure that `setUser` is defined in the **context provider**.

---

## **🎯 Summary**

✔ `useContext` **eliminates prop drilling**.  
✔ It’s useful for **theme toggling, authentication, and language settings**.  
✔ Use **Context Providers** to wrap components and provide values.  
✔ If the state updates frequently, **consider `useReducer` or state management libraries (like Redux or Zustand)**.