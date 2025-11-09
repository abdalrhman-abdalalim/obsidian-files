### ✅ Basic Usage

- Use the built-in `<Image />` component from `next/image` for optimal performance.
    
- The `src` prop should be an **object**, especially when importing statically (e.g., `import myImage from '...'`).
    
    - Inside the object: `src`, `width`, and `height` are available.
        
    - This ensures correct image rendering **after deployment**.
        

---

### 📏 Sizing

- You **must** define `width` and `height` to allow Next.js to optimize image delivery.
    
    - These values are assigned automatically for static imports.
        
    - You can **override** them manually if needed.
        
- ✅ Recommended way: use the `sizes` prop
    
    - This helps Next.js serve different image sizes depending on the viewport.
        
    - Example:
        
        `<Image    src={myImage}   sizes="(max-width: 768px) 100vw, (max-width: 1200px) 50vw, 33vw" />`
        

---

### 💤 Lazy Loading

- `loading="lazy"` is enabled by default.
    
    - It ensures the image only loads when it enters the viewport.
        

---

### ⚡ Priority Images

- Use `priority={true}` for **critical images** (e.g., hero section).
    
    - This **disables** lazy loading.
        
    - Ensures image is **preloaded** during initial page load.
        

---

### 🧱 Fill Mode

- Use `fill={true}` to make the image take **full width and height** of its parent.
    
    - The parent element must have:
        
        - `position: relative`
            
        - A defined `width` and `height`
            
    - Images in fill mode use **absolute positioning**.
        

---

### 🌍 External Images

If you're loading images from an **external source**, you need to configure Next.js to allow it.

#### In `next.config.js`:

`module.exports = {   images: {     remotePatterns: [       {         protocol: 'https',         hostname: 'example.com',         pathname: '/images/**',       },     ],   }, }`

This configuration tells Next.js to accept images from the specified external domains.