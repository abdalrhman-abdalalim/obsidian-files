### 1️⃣ From Components to Modules

- **C4 term**: “components” = building blocks inside a container.
    
- **Frontend term**: Use **"modules"** instead to avoid confusion with UI components like React components.
    
- **Definition**:
    
    - A **module** is a **top-level concern** or **major functional area** of your app.
        
    - Think of each as a **mini-application** inside your main app.
        

---

### 2️⃣ How to Identify Modules

- Look at **routes** (or likely future routes if they don’t exist yet).
    
- Use **UI specs** or **project specs** to guess possible routes.
    
- From these routes → create an **initial list of modules**.
    
- Example modules:
    
    - `Home`
        
    - `Login`
        
    - `Delivery/Pickup`
        
    - `RestaurantProfile`
        
    - `Search`
        

---

### 3️⃣ Relationship with Entities

- Some modules **align with entities** (e.g., `Restaurant` entity ↔ `Restaurant` module).
    
- But **not all modules are entities**, and **not all entities are modules**.
    
    - Example: `Search` = a big feature, but not an entity.
        
- Avoid forcing a **1-to-1 mapping** between modules and entities.
    

---

### 4️⃣ When Modules Break the Route Pattern

- Sometimes **modules live inside a route** but are **complex enough to be separate**:
    
    - Example: `MenuItems`
        
        - Lives under the `Restaurant` route.
            
        - Complex enough (options, categories, customizations) to be its own module.
            
- Some modules **don’t have their own route** at all:
    
    - Example: `ShoppingCart` → visible across pages, still a full module.
        

---

### 5️⃣ Module Implementation Reality

- **Ideal world**:
    
    - Assign each dev a module → build → done.
        
- **Real world**:
    
    - Modules will **share functionality** and **depend on each other**.
        
    - Example: `MenuItems` needs `Restaurant` data.
        
- For now: focus only on **identifying modules**.  
    Implementation & dependency management come later.
    

---

If you’d like, I can take these rules and the “FullSnack” project’s domain to **draft an initial module map** showing both route-based and non-route-based modules, so it’s visual like a C4 Level 3 diagram.  
That would make these relationships (and exceptions) much easier to see.     