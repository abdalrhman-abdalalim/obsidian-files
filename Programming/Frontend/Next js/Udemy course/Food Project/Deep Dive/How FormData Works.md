## **🛠 How `FormData` Works**

- `FormData` is a built-in browser API that collects form inputs by their `name` attributes.
- When the form is submitted, `FormData` automatically extracts the input values and sends them as key-value pairs.
- In **Next.js Server Actions**, you can use `FormData.get("inputName")` to access these values.

---

## **✅ Example: Using `FormData` in a Server Action**

```tsx
"use server";

export async function shareMeal(formData: FormData) {
  const title = formData.get("title") as string;
  const summary = formData.get("summary") as string;
  const image = formData.get("image") as File; // If input type is "file"
  const name = formData.get("name") as string;
  const email = formData.get("email") as string;
  const instructions = formData.get("instructions") as string;

  console.log({ title, summary, image, name, email, instructions });
}
```

---

## **🎯 Form Example**

```tsx
<form action={shareMeal}>
  <input type="text" name="title" required />
  <input type="text" name="summary" required />
  <input type="file" name="image" />
  <input type="text" name="name" required />
  <input type="email" name="email" required />
  <textarea name="instructions" required></textarea>
  <button type="submit">Share Meal</button>
</form>
```


📌 **How It Works:**

1. When the form is submitted, the `action={shareMeal}` automatically sends all input values as a `FormData` object.
2. The **server action (`shareMeal`)** extracts values using `formData.get("name")`.
3. If an input is a **file upload**, use `formData.get("image") as File` to access it.

---

## **🔴 Important Notes**

1. **`FormData.get()` returns `FormDataEntryValue | null`**
    - Always cast (`as string`) if you expect a string.
    - For files, use `as File` to ensure proper handling.
2. **Supports File Uploads**
    - If the input is `<input type="file" name="image" />`, `formData.get("image")` will return a `File` object.
3. **All values are strings or `File` objects**
    - You **must convert numbers manually** (`parseInt(formData.get("age") as string, 10)`).

---

## **🚀 Why Use `FormData`?**

✅ **Works natively with `<form>`**  
✅ **No need for `event.preventDefault()`**  
✅ **Supports file uploads**  
✅ **Works in Next.js Server Actions without extra API calls**

This makes **Server Actions with `FormData`** a **powerful and simple** way to handle form submissions in Next.js! 🚀