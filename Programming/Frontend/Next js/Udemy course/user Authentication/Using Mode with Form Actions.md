### ⚙️ Using Mode with Form Actions

You can use the `mode` parameter to determine the action for your form, such as handling login or signup based on the mode value:

```
export async function auth(mode, prevState, formData) {
  if (mode === 'login') {
    return login(prevState, formData);
  }
  return signup(prevState, formData);
}

// Binding mode to the function call:
const loginHandler = auth.bind(null, 'login');
const signupHandler = auth.bind(null, 'signup');
```

### 📌 Key Points for Using `bind()`

- **Context Preservation:** `bind()` creates a new function with a fixed first argument (`mode` in this case) while preserving the original function context.
    
- **Flexible Reuse:** It allows you to reuse the same function for different modes without duplicating logic.
    
- **Simplified Event Handling:** Useful for event handlers where you need to pass additional parameters.
    

### ⚠️ Key Points

- Always `await` `params` when using Next.js 15+.
    
- Use `useSearchParams()` in Client Components.
    
- Use the `URL` API in Server Components and Middleware.
    
- Be aware that search params are part of the URL, so they are publicly accessible.