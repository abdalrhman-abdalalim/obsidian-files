## **1️⃣ ensureImageDirectory Function**

### **Purpose:**

Before saving an image, we must ensure the directory where images are stored (`public/images`) exists.

```tsx
async function ensureImageDirectory() {
  try {
    await fs.mkdir(IMAGE_DIR, { recursive: true });
  } catch (error) {
    console.error("❌ Error creating images directory:", error);
  }
}
```

### **How it Works:**

- `fs.mkdir(IMAGE_DIR, { recursive: true })`
    - **Creates the `public/images` directory** (if it doesn't exist).
    - `{ recursive: true }` ensures that even if **parent directories are missing**, they get created.
- If an **error** occurs while creating the directory, it's caught and logged.

---

## **2️⃣ addMeal Function**

### **Purpose:**

This function:

- **Processes** a meal object
- **Saves the image** (if uploaded)
- **Stores the meal in `meals.json`** without deleting existing data.

---

### **Step 1: Ensure Image Directory Exists**

`await ensureImageDirectory();`

**🔹 This makes sure the `public/images` directory exists before saving an image.**

---

### **Step 2: Sanitize Meal Data**


`meal.slug = slugify(meal.title, { lower: true }); 
`meal.instructions = xss(meal.instructions);`

- `slugify(meal.title, { lower: true })`
    - **Generates a clean URL-friendly slug** from the meal title.
    - Example: `"Spaghetti Carbonara"` → `"spaghetti-carbonara"`.
- `xss(meal.instructions)`
    - **Removes any harmful JavaScript code** from instructions (prevents XSS attacks).

---

### **Step 3: Handle Image Upload**

`const imageInput = meal.image; let imageUrl = "";`

- **Extracts** the image from the meal object.
- **Prepares a variable (`imageUrl`)** to store the correct image path.

---

### **Step 4: Process the Image File**

`if (imageInput instanceof File) {`

- **Checks if the image is a File** (i.e., the user uploaded an image).
- If `imageInput` is **not a File**, it might be a URL (handled later).

---

### **Step 5: Get File Extension**

`const extension = imageInput.name.split(".").pop(); 
`if (!extension) {   throw new Error("Invalid image file."); }`

- `imageInput.name.split(".").pop();`
    - **Extracts the file extension** (e.g., `"jpg"`, `"png"`).
    - `"photo.jpg"` → `["photo", "jpg"]` → `"jpg"`.
- **If there's no extension, we throw an error** because the file is invalid.

---

### **Step 6: Generate a Proper File Name**

``const fileName = `${meal.slug}.${extension}`; 
`const filePath = path.join(IMAGE_DIR, fileName);``

- Uses **the meal slug as the filename**, ensuring a **human-readable name**.
    - Example:
        - Meal title: `"Spaghetti Carbonara"`
        - Slug: `"spaghetti-carbonara"`
        - Image: `"spaghetti-carbonara.jpg"`
- **Creates the full file path** where the image will be saved:
    - Example:  
        `public/images/spaghetti-carbonara.jpg`

---

### **Step 7: Save Image to Disk**

`const buffer = await imageInput.arrayBuffer(); 
`await fs.writeFile(filePath, Buffer.from(buffer));`

- `imageInput.arrayBuffer()`
    - **Reads the file as binary data**.
- `Buffer.from(buffer)`
    - **Converts binary data to a format suitable for saving**.
- `fs.writeFile(filePath, Buffer.from(buffer))`
    - **Saves the image in the `public/images` folder**.

---

### **Step 8: Assign Image URL to Meal**

``imageUrl = `/images/${fileName}`;``

- **Stores the correct image path** for the meal.
- Example:
    - If the file was `"spaghetti-carbonara.jpg"`
    - The image URL is `"/images/spaghetti-carbonara.jpg"`

---

### **Step 9: Handle External Image URLs**

`} else if (typeof imageInput === "string" && imageInput.startsWith("http")) {   imageUrl = imageInput; }`

- **Checks if the image is already a URL (e.g., from the internet).**
- If it's a valid URL, we **use it directly** instead of saving a new file.

---

### **Step 10: Handle Invalid Image Inputs**

`else {   throw new Error("Invalid image input. Provide a valid URL or upload a file."); }`

- If the image is **neither a File nor a valid URL**, we throw an error.

---

### **Step 11: Assign Image URL to Meal**


`meal.image = imageUrl;`

- **Ensures the correct image URL is saved** in `meals.json`.

---

### **Step 12: Read Existing Meals**

```tsx
let meals: Meal[] = [];
try {
  const rawData = await fs.readFile(FILE_PATH, "utf-8");
  meals = JSON.parse(rawData);
  if (!Array.isArray(meals)) {
    throw new Error("meals.json is corrupted or not an array.");
  }
} catch (error) {
  console.warn("meals.json not found or empty. Creating a new one.", error);
}
```

- Reads the **current `meals.json` file**.
- If the file:
    - Exists → **Parses the JSON and stores it in `meals`**.
    - **Doesn’t exist / is empty** → Initializes an **empty array (`[]`)**.

---

### **Step 13: Add the New Meal**

`meals.push(meal);`

- **Adds the new meal** to the existing list.

---

### **Step 14: Save Updated Meals to File**

`await fs.writeFile(FILE_PATH, JSON.stringify(meals, null, 2));`

- Converts `meals` back into **a JSON string**.
- Saves it **back to `meals.json`**.
- `null, 2` → **Formats the JSON file** for better readability.

---

### **Step 15: Success Message**

`console.log("✅ Meal added successfully!");`

- Logs a success message **when the meal is successfully stored**.

---

### **Step 16: Handle Errors**

`} catch (error) {   console.error("❌ Error adding meal:", error); }`

- **Catches any errors** in the entire process.
- Logs an error message if something goes wrong.

---

# ✅ **Final Summary**

### **What This Code Does?**

1. **Ensures the `/public/images/` folder exists**.
2. **Sanitizes** the meal data (slug + XSS protection).
3. **Processes image input**:
    - If it's an uploaded file → **Saves it correctly** with the meal's slug.
    - If it's an external URL → **Uses it directly**.
4. **Reads existing meals from `meals.json`**.
5. **Adds the new meal** to the list.
6. **Writes the updated list** back to `meals.json`.
7. **Logs success or errors**.

---

## **🛠️ Example Usage**

### **Scenario 1: User Uploads an Image**

```tsx
await addMeal({
  title: "Cheeseburger",
  instructions: "<script>alert('XSS')</script> Cook well!",
  image: new File(["fake-content"], "burger.jpg", { type: "image/jpeg" }),
});
```


**Result:**

- Image saved as `/public/images/cheeseburger.jpg`.
- `meals.json` gets updated with:
    
    json
    
    CopyEdit
    
    `{   "title": "Cheeseburger",   "instructions": "Cook well!",   "image": "/images/cheeseburger.jpg" }`
    

---

### **Scenario 2: User Provides an Image URL**

`await addMeal({   title: "Caesar Salad",   instructions: "Mix well and serve.",   image: "https://example.com/salad.jpg", });`

**Result:**

- No image is saved locally.
- `meals.json` stores:
    
    json
    
    CopyEdit
    
    `{   "title": "Caesar Salad",   "instructions": "Mix well and serve.",   "image": "https://example.com/salad.jpg" }`
    

---

**This function is now fully optimized for handling images and storing meals properly! 🚀**