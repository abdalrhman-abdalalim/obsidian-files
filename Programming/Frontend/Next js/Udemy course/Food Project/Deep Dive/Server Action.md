
A **Server Action** in Next.js is a function that runs **on the server** instead of the client.  
It is defined using `"use server"` and can be used **without needing an API route**.

---

### **🛠 How Server Actions Work**

1. **Declared with `"use server"`** at the top.
2. **Runs on the server**, not the client.
3. **Automatically sends a request** behind the scenes when called from a component.
4. **No need for API routes** (`app/api/...`), making the code **simpler & more efficient**.

---

### **✅ Example: Server Action to Add a Meal**

```tsx
import ImagePicker from "@/components/meals/ImagePicker";
import { Meal } from "@/interfaces";

export default function ShareMealPage() {
  async function shareMeal(formData: FormData) {
    "use server";

    const meal: Meal = {
      title: formData.get("title") as string,
      summary: formData.get("summary") as string,
      image: formData.get("image") as string,
      creator: formData.get("name") as string,
      creator_email: formData.get("email") as string,
      instructions: formData.get("instructions") as string,
      id: Math.random(),
      slug: formData.get("title") as string,
    };

    console.log(meal);
  }

  return (
    <>
      <header className="gap-12 my-12 mx-auto w-11/12 max-w-6xl text-[#ddd6cb] text-2xl">
        <h1 className="font-montserrat">
          Share your {" "}
          <span className="bg-gradient-to-r from-[#f9572a] to-[#ff8a05] bg-clip-text text-transparent">
            favorite meal
          </span>
        </h1>
        <p>Or any other meal you feel needs sharing!</p>
      </header>

      <main className="my-12 mx-auto w-11/12 max-w-6xl text-white">
        <form className="max-w-4xl" action={shareMeal}>
          <input type="text" id="name" name="name" required placeholder="Your Name" />
          <input type="email" id="email" name="email" required placeholder="Your Email" />
          <input type="text" id="title" name="title" required placeholder="Title" />
          <input type="text" id="summary" name="summary" required placeholder="Short Summary" />
          <textarea id="instructions" name="instructions" rows={10} required placeholder="Instructions"></textarea>
          <ImagePicker name="image" label="Pick your image" />
          <button type="submit">Share Meal</button>
        </form>
      </main>
    </>
  );
}
```
---

### **🚀 Why Use Server Actions?**

✅ **No API Routes Needed** → You don’t need `app/api/...` anymore.  
✅ **Better Performance** → Runs directly on the server, avoiding unnecessary client-side code.  
✅ **Secure** → Runs **only** on the server, so sensitive operations like database writes are safe.  
✅ **Handles Forms Easily** → Works directly with `FormData`, making forms cleaner and simpler.

---

### **🔴 Important Notes**

1. **Only Call from Client Components** → You can't use Server Actions inside **Server Components** directly.
2. **Must be Asynchronous** → Server Actions **must** be `async`.
3. **No Direct State Updates** → Since they run on the server, you must **revalidate the cache** (`revalidatePath`) or update the client manually.](<📌 What is a Server Action in Next.js?
