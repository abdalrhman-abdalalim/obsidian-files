## Concept

- **Request Memoization** ensures that a function's response is cached **within a single request cycle** in a React application.
- When the function is called **for the first time** in a request, its result is stored in React's cache.
- Subsequent calls to the same function **during the same request cycle** reuse the cached response instead of recomputing.
- The `cache` function from React is used to **memoize the result of a function** across a **single request cycle** (especially useful in frameworks like Next.js with Server Components).

#### 📦 How It Works

- You **wrap your data-fetching (or heavy computation) function** with `cache`.
    
- React stores the **returned value** of that function **the first time it is called** during a single request.
    
- On **subsequent calls to that function in the same request**, React **reuses the previously cached response**.
    
- This helps avoid **redundant network calls or expensive computations** when the same data is needed in multiple places during one render.

#### ✅ Benefits

- Optimizes performance by **eliminating repeated executions**.
    
- Ensures consistency of returned data **within a single request cycle**.
    
- Very useful for **custom data sources** in Server Components.

## Implementation

```jsx
import { cache } from "react";

const fetchData = cache(async (key: string) => {
  const res = await fetch(`https://api.example.com/data/${key}`);
  return res.json();
});
```


### Key Points:

1. **`cache` from React**:
    
    - Wraps the function to enable memoization.
        
    - Automatically caches the result **per request cycle**.
        
2. **Behavior**:
    
    - First call → Executes the function and stores the result.
        
    - Subsequent calls → Returns the cached result (no duplicate execution).
        
3. **Use Case**:
    
    - Avoids redundant API calls/fetching for the same data in:
        
        - Layouts
            
        - Pages
            
        - Components
            
        - Server Actions
            

## Example: Reusing Cached Data

```tsx
// Component A (first call → fetches and caches)
const dataA = await fetchData("posts");

// Component B (reuses cached data)
const dataB = await fetchData("posts");

// dataA === dataB (same request cycle)
```
## Notes

- **Cache Scope**:
    - Only persists for **one HTTP request** (e.g., a page load or API call).
    - Resets on the next request.
- **Custom Data Sources**:
    - Works with **any async function** (DB queries, API calls, etc.).
- **Limitations**:
    - Not a replacement for global state management (e.g., Redux).
    - Only optimizes **per-request** duplicate calls.