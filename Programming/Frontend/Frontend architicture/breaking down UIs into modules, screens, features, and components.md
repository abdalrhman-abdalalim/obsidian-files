Think of it as a **pyramid of granularity**:

`Module  └── Screen(s)       └── Feature(s)            └── Component(s)`

---

## 🏗️ The Buckets

1. **Module 🏢**
    
    - A **domain area** in your app (Delivery, Restaurant, Login, Search, Cart).
        
    - Can have one or more **screens**.
        
    - Example: `modules/delivery`
        

---

2. **Screen 📺**
    
    - **Entry point UI** of a module.
        
    - Sometimes just _one_ (like Delivery page).
        
    - Sometimes _many_ (like Search with multiple tabs = multiple screens).
        
    - Example: `/delivery` → `DeliveryScreen.tsx`
        

---

3. **Feature ⚙️**
    
    - A **chunk of functionality** inside a screen.
        
    - Usually **made of multiple components**.
        
    - Rule of thumb: if it’s big enough to need its own folder → it’s a feature.
        
    - Example: Restaurant Filters, Ratings & Reviews, Menu Categories.
        

---

4. **Component 🧩**
    
    - **Small, reusable building blocks**.
        
    - Buttons, Cards, Dropdowns, Inputs.
        
    - Can be composed of smaller subcomponents.
        
    - Example: `RestaurantCard`, `MenuItem`, `CategoryTag`.
        

---

5. **Shared (🖤)**
    
    - Stuff **used everywhere**, not tied to one module.
        
    - Layouts, header, footer, UI library components.
        
    - Example: `Header`, `Button`, `Modal`.
        

---

# 📊 Example: Delivery Page Breakdown

Here’s how your **Delivery module** might look when color-coded:

- **Black (Shared)** → Header, global RestaurantCard
    
- **Blue (Screen)** → DeliveryScreen
    
- **Purple (Feature)** → Filters, OffersCarousel, RestaurantsCarousel
    
- **Green (Component)** → FilterDropdown, OfferTile, CategoryCarousel
    

---

# 📝 Example: Restaurant Module Breakdown

```tsx
restaurant/
 ├── RestaurantScreen.tsx    (the one screen)
 ├── components/             (misc. small ones, not tied to features)
 │    └── FooterNotes.tsx
 └── features/
      ├── RestaurantHeader/
      │    ├── RestaurantInfo.tsx
      │    └── SearchBar.tsx
      ├── MenuCategories/
      │    └── CategoryList.tsx
      ├── MenuItems/
      │    └── MenuItem.tsx
      ├── RatingsAndReviews/
      │    ├── Ratings.tsx
      │    └── ReviewItem.tsx
      └── SidebarLayout/
           └── CategorySidebar.tsx

```

---

# 🔑 Rules of Thumb

- **If it’s a page entry → Screen.**
    
- **If it’s a big section with many parts → Feature.**
    
- **If it’s small + reusable → Component.**
    
- **If it’s used across modules → Shared.**
    
- **If naming feels generic (“sidebar”, “box”) → rename to purpose (“CategorySidebar”).**
    

---

👉 Basically:

- **Modules = chapters of your app**
    
- **Screens = pages in the chapter**
    
- **Features = paragraphs on the page**
    
- **Components = words/sentences inside the paragraphs**
    

---

Would you like me to **draw this as a diagram (boxes with colors like in TLDraw)** so it’s easier to _see_ screens → features → components for one module (e.g. Delivery)?