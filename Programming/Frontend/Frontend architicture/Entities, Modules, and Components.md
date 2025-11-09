## 1️⃣ Entities — _The “things” in your problem domain_

- **What they are (abstract)**:  
    They are the main building blocks of your **domain** — the "nouns" that exist in your application's world.  
    Example in a food delivery app:
    
    - **Restaurant**
        
    - **Customer**
        
    - **Food Item**
        
    - **Shopping Cart**
        
- **What they have**:
    
    - **Attributes**: properties like `name`, `address`, `logo`, `price`, `status`.
        
    - **Operations**: actions they can do or that can be done to them, e.g., "update menu", "place order", "track order".
        
- **How they appear in code (concrete)**:
    
    - A **Model** in MVC frameworks (fetches data, stores attributes, defines operations).
        
    - A **Class**, **Interface**, or **Type** in TypeScript.
        
    - A **Service** or **Custom Hook** in React (e.g., a hook that fetches restaurant data using React Query and provides related functions).
        

---

## 2️⃣ Modules — _The “sections” of your application_

- **What they are (abstract)**:  
    The **building blocks of your application** — each one is a logical grouping of related code that deals with a specific area.
    
    Example:
    
    - **Restaurant Module** (everything related to restaurants)
        
    - **Customer Module**
        
    - **Orders Module**
        
- **Relation to Entities**:  
    Sometimes there’s a **1-to-1** match (Restaurant Entity → Restaurant Module), but not always.
    
- **How they appear in code (concrete)**:
    
    - A **folder** in your codebase containing all related files (React components, hooks, services, etc.).
        
    - A **route** or **page** in frameworks like Next.js.
        
    - A **feature directory** in a modular architecture.
        

---

## 3️⃣ Components — _The “visual or functional parts” of the UI_

- **What they are (concrete)**:  
    The smallest visible/functional building blocks of your app’s interface.  
    They **don’t have an abstract-only definition** — they’re code from the start.
    
    Example in React:
    
    - `RestaurantCard`
        
    - `OrderStatusBadge`
        
    - `CustomerProfileForm`
        
- **How they appear in code**:
    
    - In MVC frameworks: as a **View**.
        
    - In modern frameworks like React, Vue, Svelte: as **UI components** (JSX/HTML + styling + logic for rendering).
        

---

### 💡 In short:

- **Entities** → the **things** in your app's world (abstract first, then modeled in code).
    
- **Modules** → the **organizational sections** of your app that group related logic.
    
- **Components** → the **actual UI parts** your users see and interact with.