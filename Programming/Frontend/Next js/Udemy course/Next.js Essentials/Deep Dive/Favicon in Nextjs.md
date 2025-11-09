### ✅ **Automatic Favicon Handling**

If you place an `icon.png` directly inside the `app/` directory, **Next.js will automatically use it as the favicon** without any additional configuration.

🔹 **Example:**

```plaintext
/my-project
│── /app
│   ├── page.tsx  (Main page)
│   ├── layout.tsx  (Root layout)
│   ├── icon.png  (✅ Automatically used as the favicon)
│   ├── /about
│   │   ├── page.tsx

```

✅ Next.js **automatically converts `icon.png` into different favicon sizes** and applies them to `<head>`.