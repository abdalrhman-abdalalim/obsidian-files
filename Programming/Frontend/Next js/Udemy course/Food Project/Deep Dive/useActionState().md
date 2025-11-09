`useFormState()` has been replaced by `useActionState()`. This hook is now responsible for managing the state of a component that contains a form submitted via **Server Actions**.

---

### ✅ **Key Points About `useActionState()`**

1. **It replaces `useFormState()`**.
2. **Manages state in a component with a form** that submits using **Server Actions**.
3. **Works like `useState()`** but integrates seamlessly with **Server Actions**.
4. **Takes an action function** and an **initial state**.
5. **Passes `[state, formAction]`**, which you need to use in the `<form action={formAction}>`.
6. The **function should receive form data as the second argument**, because the first argument is the **previous state**.

---

### 🔥 **Example: Using `useActionState()` with Server Actions**

```tsx
"use client";

import { useActionState } from "react";
import { experimental_useOptimistic as useOptimistic } from "react";

// Server action
async function handleSubmit(prevState: any, formData: FormData) {
  "use server";
  
  const name = formData.get("name");
  
  if (!name) {
    return { error: "Name is required!" };
  }

  return { success: `Hello, ${name}!` };
}

export default function MyForm() {
  const [state, formAction] = useActionState(handleSubmit, { success: "", error: "" });

  return (
    <form action={formAction}>
      <input type="text" name="name" placeholder="Enter your name" required />
      <button type="submit">Submit</button>

      {state.error && <p style={{ color: "red" }}>{state.error}</p>}
      {state.success && <p style={{ color: "green" }}>{state.success}</p>}
    </form>
  );
}
```


---

### 🔹 **How `useActionState()` Works Here**

1. `useActionState(handleSubmit, { success: "", error: "" })`
    - `handleSubmit`: The **server action function**.
    - `{ success: "", error: "" }`: The **initial state**.
2. `handleSubmit(prevState, formData)`
    - The **first argument** is the **previous state**.
    - The **second argument** is the **submitted `FormData`**.
3. The `form` uses **`action={formAction}`**, which is required for it to work.

---

### 🚀 **Why Use `useActionState()` Instead of `useState()`?**

- Unlike `useState()`, this hook integrates **directly with server actions**.
- **No need to manually handle state updates** after submitting the form.
- **Useful for forms that need immediate feedback**, such as validation errors.

---
