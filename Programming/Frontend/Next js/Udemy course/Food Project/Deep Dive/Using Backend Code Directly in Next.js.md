One of the powerful features of **Next.js** is the ability to use backend logic directly within your application. Instead of making API requests to an external backend, you can **read, write, and manage data** within your project using Node.js modules like `fs` (File System).

### **Example: Managing Meal Data Locally**

You can structure your backend logic in the `lib` directory and access it anywhere in your application.

#### **1️⃣ Define Your Data Handling Functions (`lib/meals.ts`)**

```tsx
import { Meal } from "@/interfaces";
import fs from "fs/promises";
import path from "path";

// Define the path to the meals.json file
const FILE_PATH = path.join(process.cwd(), "src", "data", "meals.json");

// Fetch all meals
export async function getAllMeals(): Promise<Meal[]> {
  try {
    const rawData = await fs.readFile(FILE_PATH, "utf-8");
    const parsedData = JSON.parse(rawData);
    return parsedData.meals || [];
  } catch (error) {
    console.error("Error reading meals.json:", error);
    return [];
  }
}

// Get a specific meal by slug
export async function getMeal(slug: string): Promise<Meal | undefined> {
  const meals = await getAllMeals();
  return meals.find((meal) => meal.slug === slug);
}

// Store meals in the file
export async function storeMeals(meals: Meal[]): Promise<void> {
  try {
    await fs.writeFile(FILE_PATH, JSON.stringify({ meals }, null, 2));
  } catch (error) {
    console.error("Error writing meals file:", error);
  }
}
```

---

#### **2️⃣ Using Data Without API Requests**

Instead of fetching data from an external API, you can retrieve meals **directly in your component** like this:

`const meals: Meal[] = await getAllMeals();`

This eliminates the need for **API calls**, making data access **faster and more efficient**.

---

### **💡 Why This Approach?**

✅ **Removes the need for an API** – Directly access backend logic inside your project  
✅ **Faster performance** – Avoid network latency from API calls  
✅ **Full control** – Read and write data seamlessly using Node.js
