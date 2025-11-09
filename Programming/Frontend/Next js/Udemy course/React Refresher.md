## **React Essentials** 🛠️

### **1️⃣ How React Code Works in the Browser**

- React **developer code** is transformed into **browser-compatible code** before execution.
- Browsers **do not understand JSX**, but **React compiles it** into standard JavaScript that the browser can interpret.

---

### **2️⃣ Naming Conventions in React**

- **Component Names:**
    - **Not required** to start with uppercase, but it's a **common practice**.
    - **Important:** Always name **calling components** (when used in JSX) with an **uppercase letter** to prevent conflicts with built-in HTML elements.

---

### **3️⃣ JSX Syntax Basics**

- You can **embed JavaScript expressions** inside `{ }` within JSX.
- Every **component must have a single root element** (but it can contain multiple child elements).
- Components can be **self-closing** (`<Component />`) or **open & closed** (`<Component></Component>`).

---

### **4️⃣ Styling in React**

- Use **CSS modules** for scoped styles:
	```tsx
	import classes from './comp.module.css'; <div className={classes.post}></div>
```
##### **CSS Modules (`file.module.css`)**

- **Locally scoped** styles: Each component gets its own unique class names.
- Helps **avoid conflicts** when multiple components have similar class names.

---

### **5️⃣ Event Handling Best Practices**

- Prefer naming event handler functions with `"Handler"`, e.g., `onClickHandler`.
- In JavaScript, **functions are first-class citizens** (like strings or numbers), meaning you can **pass them as props**, just like any other value.


---

### `<dialog>` Element

- The `<dialog>` HTML element is used to create **modal dialogs**.
- It has a built-in property called `open`, which **takes a Boolean value** to control visibility.
- Example:
	```tsx
	<dialog open={true}>     <p>This is a dialog.</p> </dialog>
```
    
---

## 🔹 `props.children` in React  
- `props.children` allows a component to **render JSX inside itself**.  
- It **always refers** to the content placed **between** the component’s opening and closing tags.  
- This is useful for **wrapping** or **nesting** elements inside reusable components.  

### ✨ Example:  
```tsx
const Wrapper = ({ children }) => {
    return <div className="wrapper">{children}</div>;
};

<Wrapper>
    <p>This content will be rendered inside the Wrapper component.</p>
</Wrapper>;
```

---
## 🚀 Understanding Button Behavior in Forms  

## 🔹 Default Behavior of Buttons in Forms  
- In **HTML forms**, buttons **automatically send** an HTTP request to the server when clicked.  
- This happens because the default type of a `<button>` inside a form is `"submit"`.  

## 🔹 How to Prevent Unwanted Form Submission  
- To prevent this behavior, you can **explicitly set** the `type` attribute of the button.  

### ✅ Solution: Change Button Type  
```tsx
<form>
    <button type="button">Click Me</button> <!-- Prevents form submission -->
</form>
```


--- 

##### 🔹 `event.preventDefault()` prevents the browser from generating and sending an HTTP request. This is because React is a frontend library that runs in the browser, not on the server.

---
##### 🔹 If your state depends on previous state snapshots, you should call `useState` with a function to ensure you get the latest state value.

### Correct usage:
```tsx
const [count, setCount] = useState(0);

const increment = () => {
  setCount((prevCount) => prevCount + 1);
};
```

### Why?

Passing a function to `setState` ensures that React updates the state based on the most recent value, avoiding potential issues with stale state when multiple updates occur asynchronously.

---
##### 🔹 `key` is a special built-in prop in React, and it is **not** automatically guaranteed to be unique for every element—you must ensure its uniqueness within a list.

### Correct Explanation:

The `key` prop helps React identify which items have changed, been added, or removed in a list. It **must be unique** among sibling elements to optimize re-rendering.

---

##### 🔹 In a **Single Page Application (SPA)**, pages are **not fully reloaded** like in traditional websites. Instead, JavaScript dynamically updates the **DOM (Document Object Model)** to display new content without refreshing the page.

### **Key Concepts:**

1. **Page Not "Added" but Updated:**
    
    - In an SPA, when navigating to a new route, the browser **doesn't load a new HTML file**; instead, JavaScript modifies the existing DOM to show the relevant content.
2. **How It Works:**
    
    - **React Router / Vue Router / Angular Router** handle URL changes and update components accordingly.
    - The content changes through **JavaScript DOM manipulations**, such as:
	    ```tsx
	    document.getElementById("content").innerHTML = "<h1>New Page</h1>";
```
    - Frameworks like **React, Vue, and Angular** handle this more efficiently using **Virtual DOM or Shadow DOM**.
3. **SEO & Performance Considerations:**
    
    - Since SPAs don't load new pages traditionally, **search engines** may struggle with indexing.
    - **Solution:** Use **Server-Side Rendering (SSR)** (Next.js, Nuxt.js) or **Static Site Generation (SSG)**

---

##### 🔹 If you perform **data fetching** directly inside a component **without using `useEffect`**, it can cause an **infinite loop** because the fetch operation updates the state, triggering a re-render, which then triggers another fetch, and so on.

### **Why Does This Happen?**

- When the component **renders**, it executes all top-level code, including the fetch request.
- The fetch request **updates the state** when data is received.
- Updating the state **triggers a re-render**, causing the fetch request to run **again**.
- This cycle continues indefinitely.

---

- **What is `useEffect` for?**
    
    - Handles side effects like **fetching data, updating the DOM, and subscribing to events**.
    - Prevents infinite loops by controlling when effects run using a **dependency array** (`[]`).
- **Why Shouldn't `useEffect` Return a Promise?**
    
    - If you directly return a `Promise`, React expects a cleanup function but gets an **async function instead**, causing a warning.
    - **Wrong way (causes a warning):**
        ```tsx
  useEffect(async () => {
  const data = await fetchData(); // ❌ React doesn't support async functions directly
  setState(data);
}, []);
```


---

- **Use `createBrowserRouter()`** to create the router object.
- **Pass the router object to `RouterProvider`** inside your `App` component.
- **Each route object should have a `path` and `element`** (the component to render).

```tsx
import { createBrowserRouter, RouterProvider } from "react-router-dom";
import Home from "./Home";
import About from "./About";

const router = createBrowserRouter([
  { path: "/", element: <Home /> },
  { path: "/about", element: <About /> },
]);

function App() {
  return <RouterProvider router={router} />;
}

export default App;
```

---

## **Understanding `loader` and `action` in React Router**

In your project, you are using **React Router's data APIs** (`loader` and `action`) to manage data fetching and form submissions efficiently. Let’s break it down.

---

## **1. Passing Data Using a `loader`**

A **`loader`** function is used to **fetch data** before rendering a component. The data is then accessible using `useLoaderData()`.

### **How the `loader` Works in Your Code**

- `loader` is defined in `Posts.tsx`, fetching posts from an API.
- This data is then used in `PostsList.tsx` via `useLoaderData()`.

#### **Example (`loader` in `Posts.tsx`):**

```tsx
export const loader = async () => {
  const response = await fetch("http://localhost:8080/posts");
  const posts = await response.json();
  return posts;
};
```


#### **How the Data is Used in `PostsList.tsx`:**

```tsx
const posts = useLoaderData(); // Gets posts from the loader
const postsList = posts.map((post: IProps, index: number) => (
  <Post key={index} body={post.body} author={post.author} />
));
```

#### **How the Route is Set Up in `index.tsx`:**

```tsx
{
  path: "/",
  element: <Posts />,
  loader: LoaderPosts, // Fetching data before rendering
}
```

📌 **Key Takeaways:**

- `loader` runs **before** the component renders.
- The data is **automatically available** inside `useLoaderData()`.
- Improves performance by fetching data **before rendering**.

---

## **2. Submitting Data Using `action`**

An **`action`** function handles **form submissions** without manually handling `useState` or API calls inside the component.

### **How the `action` Works in Your Code**

- The `NewPost` form submits data to `/create-post` using `POST`.
- The `action` function in `NewPost.tsx` processes the form data and sends it to the backend.

#### **Example (`action` in `NewPost.tsx`):**

```tsx
export const action = async ({ request }: { request: Request }) => {
  const formData = await request.formData();
  const post = Object.fromEntries(formData.entries());

  await fetch("http://localhost:8080/posts", {
    method: "POST",
    body: JSON.stringify(post),
    headers: {
      "Content-Type": "application/json",
    },
  });

  return redirect("/"); // Redirects to the homepage after submission
};
```

#### **How the Route is Set Up in `index.tsx`:**

```tsx
{
  path: "/create-post",
  element: <NewPost />,
  action: AddPostAction, // Handling form submission
}
```

#### **How the Form Submits Data (`NewPost.tsx`):**

```tsx
<Form method="POST" className={classes.form}>
  <textarea id="body" required rows={3} name="body" />
  <input type="text" id="name" required name="author" />
  <button>Submit</button>
</Form>
```

📌 **Key Takeaways:**

- `Form` automatically submits data using `POST` without `useState`.
- The `action` function processes form data and sends it to an API.
- After submission, it **redirects** to `/` (home) using `redirect("/")`.


---


## **🚀 How Dynamic Routes Work

Your code uses **React Router's dynamic routing** to handle post details dynamically.

### **1️⃣ Defining a Dynamic Route**

In your router configuration (`index.tsx`), you define this route:

```tsx
{
  path: ":PostId", // Dynamic route capturing PostId
  element: <PostDetails />,
  loader: DetailsLoader,
}
```


- The `:PostId` acts as a **URL parameter**.
- It matches any post ID dynamically.
- When a user navigates to `/123`, it treats `123` as `PostId`.

---

### **2️⃣ Using the Dynamic Route in the Post List**

Inside `Post.tsx`, each post links to its details page using:

```tsx
<Link to={id}>  {/* id is the dynamic PostId */}
  <p className={classes.author}>{author}</p>
  <p className={classes.text}>{body}</p>
</Link>
```


- Clicking a post navigates to `/123` (where `123` is the post ID).
- This triggers the loader function.

---

### **3️⃣ Fetching Data for a Specific Post Using `loader`**

The `PostDetails.tsx` component fetches the post dynamically:

```tsx
export const loader: LoaderFunction = async ({ params }) => {
  const response = await fetch(`http://localhost:8080/posts/${params.PostId}`);
  const resData = await response.json();
  return resData.post;
};
```

- **`params.PostId`** gets extracted from the URL (e.g., `123` from `/123`).
- The API call retrieves the specific post based on `PostId`.
- if you use loader function and you want to use params in your function use `LoaderFunction` imported from "react-router-dom" that handle type of your function

---

### **4️⃣ Displaying the Dynamic Data in `PostDetails.tsx`**

Inside `PostDetails.tsx`, you use:

```tsx
const post = useLoaderData(); // Retrieves data from the loader
```


- This ensures that when `/123` loads, it gets the post data **before rendering**.
- If the post doesn't exist, it shows an error message:
    `
```tsx
	if (!post) {
  return (
    <Modal>
      <main className={classes.details}>
        <h1>Could not find post</h1>
        <p>Unfortunately, the requested post could not be found.</p>
        <p>
          <Link to=".." className={classes.btn}>
            Okay
          </Link>
        </p>
      </main>
    </Modal>
  );
}

```
    