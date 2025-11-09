## Handle Conversation

```tsx
const { register, handleSubmit, reset } = useForm<FormData>();
  const [messages, setMessages] = useState<Imessage[]>([]);
  const sendMessage: SubmitHandler<FormData> = (data) => {
    if (data.message.trim() !== "") {
      setMessages((prev) => [
        ...prev,
        { message: data.message, type: "user" },
        { message: "Happy for helping you", type: "boot" },
      ]);
      reset();
    }
  };
  const DivRef = useRef<HTMLDivElement | null>(null);
   useEffect(() => {
    DivRef.current?.scrollIntoView({ behavior: "smooth" });
  }, [messages]);
```

### **1. `useForm<FormData>()`**

The `useForm` hook comes from [react-hook-form](https://chatgpt.com?q=react-hook-form), which simplifies form handling in React applications.  
It provides various utilities such as:

- `register` → Used to register input fields and track their values.
- `handleSubmit` → Handles form submission.
- `reset` → Resets the form fields after submission.

In this case, it's being called with a generic type `FormData`, which represents the shape of the form data.

### **2. `useState<Imessage[]>([])`**

Here, the `useState` hook is used to manage an array of messages.

- `Imessage[]` → This means the state will hold an array of objects that match the `Imessage` type.
- Initially, the `messages` array is empty (`[]`).
- `setMessages` → This function updates the `messages` state.

#### **Purpose:**

Stores a list of chat messages, including both **user messages** and **bot responses**.


### **3. `sendMessage: SubmitHandler<FormData>`**

This function handles the form submission.

#### **Breaking it down:**

`const sendMessage: SubmitHandler<FormData> = (data) => {`

- `SubmitHandler<FormData>` → This ensures the function gets the correct form data.
- `data.message` → Extracts the message input from the form.

#### **Inside the function:**

`if (data.message.trim() !== "") {`

- It checks if the message is not empty after trimming whitespace.


`setMessages((prev) => [   ...prev,   { message: data.message, type: "user" },   { message: "Happy for helping you", type: "boot" }, ]);`

- **Spreads (`...prev`) the previous messages** to retain them.
- Adds the **new user message** (`{ message: data.message, type: "user" }`).
- Adds a **bot response** (`{ message: "Happy for helping you", type: "boot" }`).

`reset();`

- **Resets the form** after submission, clearing the input field.

### **4. `useRef<HTMLDivElement | null>(null)`**

Here, `useRef` is being used to create a reference to a `<div>` element.

#### **Breaking it down:**

`const DivRef = useRef<HTMLDivElement | null>(null);`

- `useRef` is initialized with `null`.
- `HTMLDivElement | null` → This means `DivRef` will either:
    - Refer to an actual `<div>` element (`HTMLDivElement`).
    - Be `null` if it's not assigned to any element.

#### **Purpose:**

- `useRef` allows **direct access** to the DOM element.
- Common use cases:
    - **Scrolling to the latest message** in a chat.
    - **Focusing an element** dynamically.

### **Explanation of `useEffect` with `DivRef`**

This `useEffect` runs whenever the `messages` state updates.

`useEffect(() => {   DivRef.current?.scrollIntoView({ behavior: "smooth" }); }, [messages]);`

### **Breaking it Down:**

1. **`useEffect` Hook:**
    
    - Executes **side effects** in a React component.
    - Runs **after** rendering.
    - The dependency array `[messages]` means this effect **re-runs** every time `messages` change.
2. **`DivRef.current?.scrollIntoView({ behavior: "smooth" })`**
    
    - `DivRef.current` → Refers to the `<div>` element (if assigned).
    - `?.` (Optional chaining) → Ensures it doesn't throw an error if `DivRef.current` is `null`.
    - `.scrollIntoView({ behavior: "smooth" })`
        - **Scrolls the referenced div into view**.
        - `{ behavior: "smooth" }` → Adds a smooth scrolling effect.

### **Purpose:**

- Every time a new message is added to `messages`, the **chat automatically scrolls** to the latest message.
- Ensures a **seamless user experience** without manually scrolling.