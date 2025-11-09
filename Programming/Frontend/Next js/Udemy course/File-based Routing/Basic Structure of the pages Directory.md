The `pages/` folder defines the routes of your app. Each `.js`, `.jsx`, `.ts`, or `.tsx` file inside it (and its subfolders) becomes a route.

```bash
/pages
  ├── index.js         # Home route (/)
  ├── about.js         # About page (/about)
  └── products
      ├── index.js     # Products listing (/products)
      └── [id].js      # Dynamic route for individual product (/products/:id)
```

### 📄 Static Routes

- `index.js` → `/`  
    The root of the application.
    
- `about.js` → `/about`  
    A basic static route.
    
- `products/index.js` → `/products`  
    A nested static route under the `/products` path.

---

### 🔁 Dynamic Routes

- `products/[id].js` → `/products/:id`  
    This is a **dynamic route**. Square brackets `[ ]` are used to define a placeholder for the route parameter (like `id` in this case).
    
#### Example:

- `/products/123`
    
- `/products/shirt-xyz`