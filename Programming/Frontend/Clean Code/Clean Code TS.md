# Props
#### - I you write rest props for any component and nested of writing everything from scratch use this way to grip all element attributes
``` tsx
import React from "react";
interface IProps {
    className?: string;
    children: unknown[] | unknown;
    title?: string;
    onClick?: (e: React.MouseEvent) => void;
}

interface CardProps extends React.ComponentPropsWithoutRef<"div"> {}
const Test = ({ className, ...rest }: CardProps) => {

  return <div className={className} {...rest} />;

};
export default Test;
```
#### - This extends `React.ComponentPropsWithoutRef<"div">`, which means it automatically includes all the standard HTML attributes of a `<div>` (e.g., `className`, `id`, `onClick`, etc.).

#### - It’s a cleaner and more reusable way to type a component that behaves like a `<div>`.

### ✅ Pros:

- You don’t have to manually define common props like `className`, `id`, `onClick`, etc.
- More maintainable, especially when dealing with native HTML elements.
- Works seamlessly with `...rest` pattern.

---

# Generic components
- If I have component and I want to render different types in it.

### 📌 `IProps<T>` - Generic Props Interface
``` tsx
import { ReactNode } from "react";

interface IProps<T> {
    items: T[];
    renderItem: (item: T) => ReactNode;
}

```
- This interface defines a **generic** prop type.
- `T` is a generic type parameter, allowing `GenericCompnent` to work with **any data type**.
- `items: T[]` → An array of data items of type `T`.
- `renderItem: (item: T) => ReactNode` → A function that renders each item as a React element.

### 📌 `Slide` and `Author` Interfaces
```tsx
interface Slide {
    id: number;
    imageURL: string;
    caption: string;
}

interface Author {
    id: number;
    imageURL: string;
    caption: {
        title: string;
        firstName: string;
    };
}

```
- Defines two different types of objects:
    - `Slide`: Represents a **carousel slide**.
    - `Author`: Represents an **author**, with an additional nested object for `caption`.


### 📌 Sample Data Arrays
```tsx
const slides: Slide[] = [
  { id: 1, imageURL: "wsdrewr", caption: "Slide 1" },
  { id: 2, imageURL: "wsdrewr", caption: "Slide 2" },
  { id: 3, imageURL: "wsdrewr", caption: "Slide 3" },
];

const authors: Author[] = [
  {
    id: 1,
    imageURL: "wsdrewr",
    caption: { title: "Dr.", firstName: "Abdo" },
  },
  {
    id: 2,
    imageURL: "wsdrewr",
    caption: { title: "Prof.", firstName: "Ahmed" },
  },
  {
    id: 3,
    imageURL: "wsdrewr",
    caption: { title: "Mr.", firstName: "Omar" },
  },
];

```
- These arrays store sample data for **slides** and **authors**.


### 📌 `GenericCompnent<T>` - The Generic List Component
```tsx
const GenericCompnent = <T,>({ items, renderItem }: IProps<T>) => {
   return (
       <div>
           {items.map(renderItem)}
       </div>
   );
};

```
- The component:
    1. Accepts an `items` array of any type `T`.
    2. Uses `map()` to apply `renderItem` to each item.
    3. Wraps everything in a `<div>`.

**✅ This allows us to reuse this component with different types of data!**


### 📌 Using `GenericCompnent` in `App`
``` tsx
const App = () => {
    return (
        <GenericCompnent<Author>
            items={authors}
            renderItem={(auth) => (
                <h1>{auth.caption.firstName}</h1>
            )}
        />
    );
};

```
- This renders a list of authors by displaying their `firstName` inside `<h1>` tags.

---

# Type Narrowing
 
 can render either a `<button>` or an `<a>` (anchor) element depending on the props it receives. It uses **TypeScript type narrowing** to distinguish between the two possible prop types. Let's break it down step by step.
## **🛠️ Why Use Type Narrowing?**

- Prevents TypeScript errors when spreading props (`<button {...props}/>` would break if `href` existed).
- Ensures correct types for `<a>` and `<button>` without needing separate components.
- Makes the code **cleaner**, **reusable**, and **type-safe**.

🚀 **This is a great pattern for polymorphic components in TypeScript React!**


### 1️⃣ Defining Prop Types
```tsx
type ButtonProps = {
    children: string;
    onClick: () => void;
}

type AnchorProps = {
    href: string;
    target: string;
    rel: string;
}
```
- `ButtonProps` is for a **button** element:
    
    - Requires `children` (a string).
    - Requires an `onClick` function.
- `AnchorProps` is for an **anchor (`<a>`)** element:
    
    - Requires `href`, `target`, and `rel` attributes.


### 2️⃣ Type Guard Function
```tsx
function isPropsForAnchor(props: ButtonProps | AnchorProps): props is AnchorProps {
    return "href" in props;
}
```
- This function **checks if `props` contains `href`**.
- If `href` exists, it assumes `props` is of type `AnchorProps`.
- It returns `true` if `props` is an **anchor** and `false` otherwise.
- This function helps **TypeScript correctly infer the type of `props`** inside the component.


### 3️⃣ Functional Component with Type Narrowing
```tsx
[function isPropsForAnchor(props: ButtonProps | AnchorProps): props is AnchorProps {
    return "href" in props;
}](<const TypeNarrowingCleanCode = (props: ButtonProps | AnchorProps) =%3E {
    if (isPropsForAnchor(props)) {
        return %3Ca {...props} />
    }
    else {
        return <button {...props}/>
    }
}>)
```
- The component receives `props`, which could be either `ButtonProps` or `AnchorProps`.
- It calls `isPropsForAnchor(props)` to determine whether it should render an `<a>` tag.
- If `isPropsForAnchor(props)` returns **true**:
    - `props` is treated as `AnchorProps`.
    - It spreads all `AnchorProps` attributes into an `<a>` element.
- Otherwise:
    - `props` is treated as `ButtonProps`.
    - It spreads all `ButtonProps` attributes into a `<button>` element.


#### 🎯 Example Usage
```tsx
<TypeNarrowingCleanCode href="https://example.com" target="_blank" rel="noopener noreferrer" />

// render this :obs_down_arrow_with_tail:

<a href="https://example.com" target="_blank" rel="noopener noreferrer"></a>
```

```tsx
<TypeNarrowingCleanCode onClick={() => alert("Clicked!")}>Click me</TypeNarrowingCleanCode>

// render this :obs_down_arrow_with_tail:

<button>Click me</button>
```


---
# EventHandlers

This code defines a **React functional component** called `EventHandlers`, which takes two event handler props:

- `onClick` → A function for handling button clicks.
- `onChange` → A function for handling input field changes.
## **1️⃣ Interface for Props (`IProps`)**

```tsx
interface IProps {     onClick: React.MouseEventHandler<HTMLButtonElement>;     onChange: React.ChangeEventHandler<HTMLInputElement>; }`
```
- This **TypeScript interface** ensures that `onClick` and `onChange` are of the correct types:
    - `onClick` → Handles mouse click events on a `<button>`.
    - `onChange` → Handles input change events on an `<input>`.

**✅ Benefit:**

- Improves **type safety** by making sure that the correct event handlers are passed.
- Prevents potential **runtime errors** due to incorrect function signatures.


## 2️⃣ Defining Event Handler Functions

```tsx
const handleClick: React.MouseEventHandler<HTMLButtonElement> = (event) => { console.log('Button clicked', event); };
```
```tsx
const handleChange: React.ChangeEventHandler<HTMLInputElement> = (event) => { console.log("button changed"); };
```
- `handleClick` → Logs the button click event.
- `handleChange` → Logs the input value when the user types.
- event will auto take the right type 

**✅ Benefit:**

- **Single Responsibility Principle (SRP)**:
    - These functions are **independent** and can be reused across multiple components.
    - Easier to **test**, **modify**, and **extend** in the future.

## 3️⃣ The `EventHandlers` Component - Reusable and Maintainable
```tsx
const EventHandlers = ({ onClick, onChange }: IProps) => { return( 
<div> 
<button onClick={onClick}>Click me</button> <input type="text" onChange={onChange} /> </div> ); };
```
- Uses **destructuring** to extract `onClick` and `onChange` from props.
- Renders:
    - A `<button>` with `onClick` attached.
    - An `<input>` field with `onChange` attached.

**✅ Benefits:**

1. **Encapsulated Logic**
    
    - The component **does not define event handlers inside the JSX**, making it **cleaner and more reusable**.
2. **Dependency Injection**
    
    - The handlers are passed **as props**, meaning different behaviors can be injected from parent components.
3. **Separation of Concerns**
    
	    - UI (`JSX markup`) is separate from **event handling logic**, making the code easier to **read** and **debug**.