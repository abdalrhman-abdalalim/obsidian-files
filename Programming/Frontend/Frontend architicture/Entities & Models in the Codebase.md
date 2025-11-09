## 1. 🌍 What are Entities?

- **Definition:**  
    Entities are the **core concepts** of your business/domain.
    
    - Example in "Full Snack" system:
        
        - `Restaurant`, `Customer`, `ShoppingCart`, `MenuItem`.
            
- **Why Important:**
    
    - They exist **everywhere** in the system (DB, API, UI).
        
    - If you model them wrong → كل حاجة فوقها هتتهز.
        
    - Think of them like **DNA** → كل جزء في الجسم (المشروع) مبني عليها.
        

---

## 2. 📦 Raw API Problem

Normally, your backend exposes **REST endpoints**:

- `/restaurants/:id`
    
- `/restaurants/:id/categories`
    
- `/restaurants/:id/reviews`
    

When you fetch them directly:

- Data shape = **ugly, nested, incomplete, noisy**.
    
    - Example:
        
        ```tsx
		        {
		  "data": {
		    "attributes": {
		      "name": "Pizza House",
		      "offersDelivery": true,
		      "offersPickup": true
		    },
		    "relationships": {
		      "categories": {
		        "data": [
		          { "id": 1, "name": "Italian" }
		        ]
		      }
		    }
		  }
		}
		
		```
        
- Problems:
    
    1. Too many levels (`attributes`, `relationships`).
        
    2. Contains extra stuff you don’t need (IDs, irrelevant fields).
        
    3. Missing info (category name sometimes incomplete).
        

If you use this **as-is in React components** →

- Components become messy.
    
- Every time backend changes API → you break everywhere.
    
- Hard to reuse.
    

---

## 3. 🧰 The Model Layer (The Magic Sauce)

So, what do we do? We **introduce a layer in the middle**:

### ✅ Steps:

1. **Define Types (TS/Interfaces):**
    
    ```tsx
    type Restaurant = {
  id: string
  name: string
  categories: string[]
  rating: number
  reviews: Review[]
}

type Review = {
  author: string
  comment: string
  score: number
}

```
    
    ➝ This represents exactly what **frontend cares about**, no more, no less.
    
2. **Create Fetch Helpers:**
    
    - `fetchRestaurant(id)` → raw API call.
        
    - `fetchCategories(id)` → raw API call.
        
    - `fetchReviews(id)` → raw API call.
        
3. **Create Model Function (Aggregator):**
    
    ```tsx
    async function getRestaurant(id: string): Promise<Restaurant> {
  const raw = await fetchRestaurant(id)
  const cats = await fetchCategories(id)
  const reviews = await fetchReviews(id)

  return {
    id: raw.data.id,
    name: raw.data.attributes.name,
    categories: cats.map(c => c.name),
    rating: raw.data.attributes.rating,
    reviews: reviews.map(r => ({
      author: r.attributes.author,
      comment: r.attributes.comment,
      score: r.attributes.score
    }))
  }
}

```
    
    ➝ Now you have a **clean object** to give to components.
    

---

## 4. 🎭 Example: Ratings Entity

- Two endpoints:
    
    - `/restaurants/:id` → gives `rating` + `numberOfRatings` + 3 reviews.
        
    - `/restaurants/:id/reviews` → gives full reviews.
        
- Model function:
    
    ```tsx
    async function getRestaurantRatings(id: string): Promise<Ratings> {
  const rest = await fetchRestaurant(id)
  const reviews = await fetchReviews(id)

  return {
    rating: rest.data.attributes.rating,
    numberOfRatings: rest.data.attributes.numberOfRatings,
    reviews: reviews.map(r => ({
      author: r.attributes.author,
      comment: r.attributes.comment,
      score: r.attributes.score
    }))
  }
}

```
    
- UI usage:
    
    `const ratings = await getRestaurantRatings(1) return <RatingsComponent data={ratings} />`
    

---

## 5. ⚡ Why This Matters (Benefits)

- **Consistency:** All components receive the same entity shape.
    
- **Flexibility:** Backend can change → just update model function, not 50 components.
    
- **Simplicity:** Components only care about rendering, not API structure.
    
- **Aggregation:** You can combine multiple endpoints into one clean object.
    

---

## 6. 🛡️ Guardrails for Large Codebase

As project grows, chaos enters 😅 → لازم نتحكم.

### Tools:

1. **Dependency Cruiser** → prevents cross-module imports (keeps modules isolated).
    
    - Eg: `Search` module shouldn’t import stuff from `Restaurant` module.
        
2. **Commonality** (for monorepos) → checks ownership + prevents circular deps.
    
3. **Bundle Size tool** → sets max JS bundle size to avoid slow pages.
    
4. **Performance Budgets** → enforce page load < 1s, images under limit, etc.
    
5. **SonarLint** → checks code complexity, warns if function = too big or messy.
    

---

## 7. 📊 Flow Summary

```tsx
API (messy data)
      ↓
 Fetch helpers (raw fetch)
      ↓
   Model layer (clean shape)
      ↓
   Features (business logic)
      ↓
 Components (UI rendering)

```

---

💡 الفكرة الكبيرة:  
**Model = translator between backend world and frontend world.**  
Backend speaks "ugly JSON", frontend wants "pretty TS objects".  
This layer = keeps your app clean, scalable, and future-proof.