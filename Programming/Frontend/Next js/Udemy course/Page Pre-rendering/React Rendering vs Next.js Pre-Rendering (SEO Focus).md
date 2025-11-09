## 1. ⚛️ React (Client-Side Rendering - CSR)

### 🔧 How It Works

- React renders content **on the client**.
    
- Browser downloads a **minimal HTML shell** and **JavaScript bundle**.
    
- Then React fetches data and renders the UI dynamically in the browser.
    

### ⚠️ SEO Impact

- Crawlers may see **empty HTML** before JavaScript runs.
    
- Can result in **poor indexing** or missing content in search engines.
    

### ❌ Problem

- HTML is mostly empty initially.
    
- Search engines may not wait for JS to finish rendering.
    

---

## 2. 🚀 Next.js Pre-Rendering (SEO-Optimized)

Next.js improves SEO by **pre-rendering pages to HTML** before sending them to the client.

### ✅ Benefits

- Delivers **fully populated HTML**.
    
- Improves **SEO** and **page speed**.
    
- Two main types:
    
    - **Static Generation (SSG)**
        
    - **Server-Side Rendering (SSR)**