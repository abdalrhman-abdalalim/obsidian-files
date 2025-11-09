# **🚀 `useReducer` in React: A Deep Dive**

`useReducer` is a React Hook that **manages complex state logic** in a more structured way than `useState`. It is particularly useful for handling state updates that depend on previous state values.

---

## **🔗 Syntax**

`const [state, dispatch] = useReducer(reducer, initialState);`

- `reducer`: A **pure function** that defines **how the state should change** based on an action.
- `initialState`: The starting value of the state.
- `state`: The **current** state value.
- `dispatch`: A **function** used to send actions to update the state.

---

## **🛠️ Example 1: Basic Counter with `useReducer`**

Instead of using `useState`, we manage state updates using `useReducer`.

```tsx
import { useReducer } from "react";

// Reducer function
function reducer(state: number, action: { type: string }) {
  switch (action.type) {
    case "increment":
      return state + 1;
    case "decrement":
      return state - 1;
    case "reset":
      return 0;
    default:
      return state;
  }
}

export default function Counter() {
  const [count, dispatch] = useReducer(reducer, 0);

  return (
    <div>
      <h2>Count: {count}</h2>
      <button onClick={() => dispatch({ type: "increment" })}>➕ Increase</button>
      <button onClick={() => dispatch({ type: "decrement" })}>➖ Decrease</button>
      <button onClick={() => dispatch({ type: "reset" })}>🔄 Reset</button>
    </div>
  );
}
```

### **🔍 How It Works?**

1. The `reducer` function **handles state updates** based on the `action.type`.
2. `dispatch({ type: "increment" })` sends an action to update the state.
3. The component **re-renders only when the state changes**.

---

## **🛠️ Example 2: Managing an Object State**

Instead of multiple `useState` calls, `useReducer` **organizes state updates in a single function**.

```tsx
import { useReducer } from "react";

type StateType = {
  count: number;
  step: number;
};

type ActionType =
  | { type: "increment" }
  | { type: "decrement" }
  | { type: "setStep"; payload: number }
  | { type: "reset" };

// Reducer function
function reducer(state: StateType, action: ActionType): StateType {
  switch (action.type) {
    case "increment":
      return { ...state, count: state.count + state.step };
    case "decrement":
      return { ...state, count: state.count - state.step };
    case "setStep":
      return { ...state, step: action.payload };
    case "reset":
      return { count: 0, step: 1 };
    default:
      return state;
  }
}

export default function CounterWithStep() {
  const [state, dispatch] = useReducer(reducer, { count: 0, step: 1 });

  return (
    <div>
      <h2>Count: {state.count}</h2>
      <input
        type="number"
        value={state.step}
        onChange={(e) => dispatch({ type: "setStep", payload: Number(e.target.value) })}
      />
      <button onClick={() => dispatch({ type: "increment" })}>Increase</button>
      <button onClick={() => dispatch({ type: "decrement" })}>Decrease</button>
      <button onClick={() => dispatch({ type: "reset" })}>Reset</button>
    </div>
  );
}
```

### **🔍 Key Benefits**

✔ All state updates **are managed in one place (reducer)**.  
✔ `dispatch` triggers state changes in a **predictable way**.  
✔ Better **separation of logic** compared to `useState`.

---

## **🛠️ Example 3: Using `useReducer` with `useContext` (Global State)**

A common pattern is to **use `useReducer` with `useContext`** to create a global state.

### **1️⃣ Create the Context and Reducer**

```tsx
import { createContext, useReducer, ReactNode, useContext } from "react";

// Define the shape of the state
const initialState = { count: 0 };

// Reducer function
function reducer(state: typeof initialState, action: { type: string }) {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    case "decrement":
      return { count: state.count - 1 };
    default:
      return state;
  }
}

// Create context
const CounterContext = createContext<{
  state: typeof initialState;
  dispatch: React.Dispatch<{ type: string }>;
} | null>(null);

// Context Provider Component
export function CounterProvider({ children }: { children: ReactNode }) {
  const [state, dispatch] = useReducer(reducer, initialState);
  return <CounterContext.Provider value={{ state, dispatch }}>{children}</CounterContext.Provider>;
}
```


### **2️⃣ Consume the Context in Components**

```tsx
export function CounterDisplay() {
  const counterContext = useContext(CounterContext);
  if (!counterContext) throw new Error("CounterContext not found");

  return <h2>Count: {counterContext.state.count}</h2>;
}

export function CounterButtons() {
  const counterContext = useContext(CounterContext);
  if (!counterContext) throw new Error("CounterContext not found");

  return (
    <>
      <button onClick={() => counterContext.dispatch({ type: "increment" })}>➕ Increase</button>
      <button onClick={() => counterContext.dispatch({ type: "decrement" })}>➖ Decrease</button>
    </>
  );
}
```
### **3️⃣ Use in App**

```tsx
import { CounterProvider, CounterDisplay, CounterButtons } from "./CounterContext";

export default function App() {
  return (
    <CounterProvider>
      <CounterDisplay />
      <CounterButtons />
    </CounterProvider>
  );
}
```

### **🔍 Why Use `useReducer` + `useContext`?**

✔ **Centralized state management**  
✔ **Avoid prop drilling**  
✔ **More scalable than `useState` for large apps**

---

## **🚀 When Should You Use `useReducer`?**

✅ **Use `useReducer` for:**

1. **Complex state logic** (when multiple state values depend on each other)
2. **Multiple state updates based on different actions**
3. **When you need `useState`, but the logic becomes hard to manage**
4. **Global state management** (especially with `useContext`)

❌ **Avoid `useReducer` when:**

1. **Your state logic is simple** (use `useState` instead)
2. **Performance optimization isn’t needed** (sometimes `useReducer` can add unnecessary complexity)

---

## **📌 Common Mistakes & Fixes**

### **❌ Forgetting to Return State in the Reducer**

```tsx
function reducer(state, action) {
  if (action.type === "increment") {
    state.count += 1; // ❌ Directly modifying state (WRONG)
  }
}
```


✅ **Fix:** Always **return a new state object**.

```tsx
function reducer(state, action) {
  if (action.type === "increment") {
    return { ...state, count: state.count + 1 }; // ✅ Correct
  }
}
```

### **❌ Using `useState` When `useReducer` Is Better**

`const [count, setCount] = useState(0); const [step, setStep] = useState(1);`

✅ **Fix:** Use `useReducer` for **better structure**.

`const [state, dispatch] = useReducer(reducer, { count: 0, step: 1 });`

---

## **🎯 Summary**

✔ `useReducer` **manages complex state updates** in a structured way.  
✔ Ideal for **handling multiple state values** in one function.  
✔ Works great with **`useContext` for global state management**.  
✔ Avoid **overcomplicating simple state logic** with `useReducer`.


## **When to Use `useReducer`**

### **1. Complex State Logic**

- When the state has multiple sub-values or nested structures.
- Example: Managing a form where each field has validation rules.

### **2. State Transitions Depend on Previous State**

- When the next state is derived from the previous state.
- Example: A counter with **increment, decrement, and reset** actions.

### **3. Multiple Actions Affecting State**

- When different actions modify the state in different ways.
- Example: A todo app with **ADD_TODO, TOGGLE_TODO, and DELETE_TODO** actions.

### **4. Centralized State Management**

- To keep state logic in one place (the reducer function) instead of scattered `useState` calls.

### **5. Better Debugging and Testing**

- Since reducers are **pure functions**, they are easier to test and debug.
- Example: Logging actions and state changes to track how state evolves.

### **6. Performance Optimization**

- Avoids unnecessary re-renders by passing `dispatch` instead of multiple state-updating callbacks.

#### example about it : 
```tsx
import { useReducer, useState } from "react";
import About from "./About";
import { context } from "./context";
import "./styles.css";

type Taction = {
  type: "increasment" | "decreament";
};

type Tstate = {
  counter: number;
  error: null | string;
};

export default function App() {
  const reducer = (state: Tstate, action: Taction) => {
    const { type } = action;
    switch (type) {
      case "increasment": {
        const newCounter = state.counter + 1;
        const hasError = newCounter > 15;
        return {
          ...state,
          counter: newCounter > 15 ? state.counter : newCounter,
          error: hasError ? "maximum Reached!!" : null,
        };
      }
      case "decreament": {
        const newCounter = state.counter - 1;
        const hasError = newCounter < 0;
        return {
          ...state,
          counter: newCounter < 0 ? state.counter : newCounter,
          error: hasError ? "minimum Reached!!" : null,
        };
      }
      default:
        return state;
    }
  };

  const [state, dispatch] = useReducer(reducer, {
    counter: 0,
    error: null,
  });

  return (
    <div className="App">
      {state.error && <p style={{ color: "red" }}>{state.error}</p>}
      <h1>my counter is {state.counter}</h1>
      <button onClick={() => dispatch({ type: "increasment" })}>
        Increasement
      </button>
      <button onClick={() => dispatch({ type: "decreament" })}>
        decreament
      </button>
    </div>
  );
}
```
