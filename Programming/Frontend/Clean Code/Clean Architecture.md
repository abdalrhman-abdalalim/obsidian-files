In a **Next.js Clean Architecture** setup, you can follow **Robert C. Martin's Clean Architecture** principles by dividing your project into **five main layers**:

---

# **📂 Clean Architecture in Next.js**

Each layer has a clear responsibility:

```txt
/src/infrastructure
├── api/
│   ├── productApi.ts  (Fetch products from an API)
│   ├── orderApi.ts  (Fetch orders)
├── db/
│   ├── prisma.ts  (Database connection)
├── auth/
│   ├── clerkAuth.ts  (Clerk authentication logic)
```

---

## **1️⃣ Infrastructure Layer (Frameworks & Drivers)**

💡 **Handles communication with external systems like databases, APIs, and third-party services.**

✅ **Includes:**

- Database (e.g., Prisma, MongoDB, PostgreSQL)
- API clients (e.g., Axios, Fetch)
- Authentication (e.g., Clerk, NextAuth)

📌 **Example folder structure:**

```pgsql
/src/infrastructure
├── api/
│   ├── productApi.ts  (Fetch products from an API)
│   ├── orderApi.ts  (Fetch orders)
├── db/
│   ├── prisma.ts  (Database connection)
├── auth/
│   ├── clerkAuth.ts  (Clerk authentication logic)

```


🔹 **Example:**

```ts
// infrastructure/api/productApi.ts
import axios from "axios";

export const fetchProducts = async () => {
  const response = await axios.get("/api/products");
  return response.data;
};
```

---

## **2️⃣ Interface Adapters Layer**

💡 **Transforms data between the external world (UI, API, DB) and business logic.**

✅ **Includes:**

- Controllers (handling API requests)
- Mappers (converting data between layers)
- View models (shaping UI data)

📌 **Example folder structure:**

```bash
/src/adapters
├── controllers/
│   ├── productController.ts
├── mappers/
│   ├── productMapper.ts
```

🔹 **Example:**

```ts
// adapters/controllers/productController.ts
import { fetchProductsUseCase } from "@/application/usecases/fetchProducts";

export async function getProducts(req, res) {
  try {
    const products = await fetchProductsUseCase();
    res.status(200).json(products);
  } catch (error) {
    res.status(500).json({ message: error.message });
  }
}
```

---

## **3️⃣ Application Layer (Use Cases & Services)**

💡 **Contains business logic (use cases) that drive the app’s functionality.**

✅ **Includes:**

- Use cases (e.g., FetchProducts, CreateOrder)
- Business rules that orchestrate operations
- No UI, DB, or API dependencies

📌 **Example folder structure:**

```bash
/src/application
├── usecases/
│   ├── fetchProducts.ts
│   ├── createOrder.ts
├── services/
│   ├── orderService.ts
```

🔹 **Example:**

```ts
// application/usecases/fetchProducts.ts
import { ProductRepository } from "@/domain/repositories/ProductRepository";

export async function fetchProductsUseCase() {
  return ProductRepository.getAll();
}
```


---

## **4️⃣ Domain Layer (Entities & Business Logic)**

💡 **Defines the core business rules and domain models.**

✅ **Includes:**

- Entities (e.g., Product, Order)
- Repository interfaces (e.g., `ProductRepository`)

📌 **Example folder structure:**

```bash
/src/domain
├── entities/
│   ├── Product.ts
│   ├── Order.ts
├── repositories/
│   ├── ProductRepository.ts
│   ├── OrderRepository.ts
```


🔹 **Example:**

```ts
// domain/entities/Product.ts
export class Product {
  constructor(
    public id: string,
    public name: string,
    public price: number
  ) {}

  getFormattedPrice() {
    return `$${this.price.toFixed(2)}`;
  }
}
```

---

## **5️⃣ Entry Points (Next.js API & UI)**

💡 **Handles user interactions and API requests.**

✅ **Includes:**

- API routes (Next.js **App Router** or **Pages Router**)
- UI components (React components)

📌 **Example folder structure (App Router):**

```bash
/app
├── api/
│   ├── products/
│   │   ├── route.ts
├── _components/
│   ├── ProductCard.tsx
│   ├── Navbar.tsx
```


🔹 **Example API Route in Next.js App Router:**

```ts
// app/api/products/route.ts
import { getProducts } from "@/adapters/controllers/productController";

export async function GET(req: Request) {
  return getProducts(req, new Response());
}
```

---

# **🔥 Final Project Structure**

```bash
/src
├── infrastructure/  (Frameworks & Drivers)
│   ├── api/
│   ├── db/
│   ├── auth/
├── adapters/        (Interface Adapters)
│   ├── controllers/
│   ├── mappers/
├── application/     (Use Cases & Services)
│   ├── usecases/
│   ├── services/
├── domain/          (Entities & Business Logic)
│   ├── entities/
│   ├── repositories/
├── app/             (Next.js Entry Points & UI)
│   ├── api/
│   ├── _components/
```

---

# **✅ Benefits of This Clean Architecture**

✔ **Scalable & Maintainable** – Easy to add new features without affecting other layers.  
✔ **Testability** – Business logic can be tested without UI or database dependencies.  
✔ **Separation of Concerns** – UI, business rules, and data access are independent.  
✔ **Flexible Infrastructure** – You can switch database or APIs without affecting logic.