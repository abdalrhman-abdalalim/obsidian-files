### 1. **Named Components (Non-generic names)**

- ممنوع تسمي Component زي `Box`, `Thing`, `Wrapper`… إلخ.
    
- سميها باللي هي فعلًا بتمثله:
    
    - ✅ `UserCard`, `ProductList`, `CheckoutButton`
        
    - ❌ `MyComponent`, `Container`, `Stuff`
        

ليه؟ → ده بيخلي الكود **واضح، مفهوم، وقابل لإعادة الاستخدام** من غير ما تبص جوا كل ملف.

---

### 2. **Feature Isolation (Isolation principle)**

- أي **feature module** بيكون self-contained.
    
- الـ **Component** بيهتم بالـ UI فقط.
    
- الـ **Logic / fetching functions** تبقى في مكان منفصل داخل نفس الـ feature.
    

مثال:

`features/  └── user/      ├── components/      │   └── UserModal.tsx   // UI فقط      ├── api/      │   └── user.api.ts     // fetching functions      └── model/          └── user.model.ts   // data shape + abstraction`

---

### 3. **App Layer (Routing only)**

- الـ `app/` في Next.js أو `pages/` → وظيفتها الوحيدة **توصيل routes** بالـ features.
    
- يعني:
    
    - `/users` → يستورد ويعرض `UsersPage` من `features/user`
        
    - `/checkout` → يستورد `CheckoutPage` من `features/checkout`
        

ليه؟ → عشان الـ `app/` ميكونش مليان logic، يبقى مجرد **Entry point**.

---

### 4. **Modules (Isolated, No Inter-dependency)**

- كل module مستقل عن التاني.
    
- مثال: `user` مايعتمدش على `restaurant` بشكل مباشر.
    
- لو فيه data مشتركة → تتحط في `shared/` (مثلاً utilities أو components عامة).
    

---

### 5. **API Layer (lib/api.ts)**

- مكان موحد تكتب فيه **api client** (axios instance مثلًا).
    
- يبقى عندك ملف `api.ts` فيه:
    

`import axios from "axios";  export const api = axios.create({   baseURL: process.env.NEXT_PUBLIC_API_URL, });`

---

### 6. **API Functions (feature-specific)**

- جوه كل feature → تعمل ملف `*.api.ts` فيه الـ API calls الخاصة بيه.
    

``// features/user/api/user.api.ts import { api } from "@/lib/api"; import { UserResponse } from "../types/user.types";  export async function getUser(id: string): Promise<UserResponse> {   const { data } = await api.get(`/users/${id}`);   return data; }``

---

### 7. **Types Layer**

- `types.ts` بيحتوي الـ types الخاصة بالـ API Response.
    
- أمثلة:
    

`// features/user/types/user.types.ts export interface UserResponse {   id: string;   name: string;   email: string; }`

---

### 8. **Models Layer**

- هنا بتحط:
    
    1. **شكل البيانات النهائي اللي هتستخدمه جوه الـ UI**
        
    2. **Abstraction layer**: تحويل response من API → شكل جاهز للـ frontend.
        

مثال:

`// features/user/model/user.model.ts import { UserResponse } from "../types/user.types";  export interface User {   id: string;   fullName: string; }  export function toUser(response: UserResponse): User {   return {     id: response.id,     fullName: response.name,   }; }`

- كده لو غيرت الـ API، UI بتاعك مش هيتأثر غير في الـ model بس.
    

---

### 9. **Shared Components**

- لو في components بتتكرر بين modules → تتحط في `shared/components/`.
    
- أمثلة: `Button`, `Modal`, `Loader`.
    

---

### 10. **Golden Rules**

- Component = UI فقط
    
- API call = جوه `*.api.ts`
    
- Types = في `types.ts`
    
- Model = تحويل response → custom data structure
    
- Modules = منعزلة عن بعضها
    
- App = routes بس
    

---

💡 الفايدة من النظام ده:

- الكود نظيف + منظم
    
- سهل تعمل **refactor**
    
- سهل تعمل **test**
    
- أي developer جديد يقدر يدخل ويفهم بسرعة