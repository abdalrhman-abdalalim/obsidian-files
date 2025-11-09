# Docs: Using `getLayout` with Next.js + React Query

## 🎯 الفكرة العامة

في Next.js ساعات بنحتاج **Layouts مختلفة** للصفحات (مثلاً: Layout عام للمستخدم العادي، Layout خاص للـ Admin Dashboard).  
الطريقة الافتراضية في Next.js إن كل صفحة بتاخد نفس `_app.tsx`، بس باستخدام `getLayout` نقدر نخلي كل صفحة تحدد Layout بتاعها.

كمان إحنا مستخدمين **React Query** لإدارة الـ API state، فبنغلف كل حاجة بـ `QueryClientProvider`.

---

## 📦 المكتبات المطلوبة

- Next.js
    
- React Query (`react-query`)
    
- React (Typescript recommended)
    

---

## 🛠️ خطوات الحل

1. **تعريف نوع الصفحة**:  
    نضيف نوع جديد للصفحة فيه `getLayout` (اختياري).
    
    `type NextPageWithLayout = {   getLayout?: (page: ReactElement) => ReactNode; };`
    
2. **تعريف نوع AppProps**:  
    نعدل `AppProps` الأصلي ونضيف له `NextPageWithLayout`.
    
    `type AppPropsWithLayout = AppProps & {   Component: NextPageWithLayout; };`
    
3. **تجهيز React Query Client**:  
    نعمل `QueryClient` ونضيفه داخل `QueryClientProvider`.
    
    `const queryClient = new QueryClient({   defaultOptions: {     queries: {       refetchOnWindowFocus: false,       retry: 1,     },   }, });`
    
4. **إضافة getLayout في App**:
    
    - لو الصفحة عندها `getLayout` → نستخدمه.
        
    - لو معندهاش → نستخدم Layout افتراضي (مثلاً `PublicLayout`).
        
    
    `const getLayout =   Component.getLayout ?? ((page) => <PublicLayout>{page}</PublicLayout>);`
    
5. **الـ Return النهائي**:
    
    `return (   <QueryClientProvider client={queryClient}>     {getLayout(<Component {...pageProps} />)}   </QueryClientProvider> );`
    

---

## 🧩 كود مثال كامل

`// pages/_app.tsx import type { AppProps } from "next/app"; import { QueryClient, QueryClientProvider } from "react-query"; import { ReactElement, ReactNode } from "react"; import "@/common/styles/globals.css"; import PublicLayout from "@/common/components/Layouts/PublicLayout/PublicLayout";  // 1. Define type for page with layout type NextPageWithLayout = {   getLayout?: (page: ReactElement) => ReactNode; };  // 2. Extend AppProps type AppPropsWithLayout = AppProps & {   Component: NextPageWithLayout; };  export default function App({ Component, pageProps }: AppPropsWithLayout) {   // 3. Create query client   const queryClient = new QueryClient({     defaultOptions: {       queries: {         refetchOnWindowFocus: false,         retry: 1,       },     },   });    // 4. Get layout or fallback   const getLayout =     Component.getLayout ?? ((page) => <PublicLayout>{page}</PublicLayout>);    // 5. Wrap with React Query   return (     <QueryClientProvider client={queryClient}>       {getLayout(<Component {...pageProps} />)}     </QueryClientProvider>   ); }`

---

## 🖼️ مثال صفحة بتستخدم Layout خاص

`// pages/dashboard.tsx import { ReactElement } from "react"; import DashboardLayout from "@/common/components/Layouts/DashboardLayout";  function DashboardPage() {   return <h1>Welcome to Dashboard</h1>; }  // هنا بنحدد إن الصفحة دي تستخدم DashboardLayout DashboardPage.getLayout = function getLayout(page: ReactElement) {   return <DashboardLayout>{page}</DashboardLayout>; };  export default DashboardPage;`

لو الصفحة **مفيهاش `getLayout`** → هتشتغل تلقائي بـ `PublicLayout`.

---

✅ كده عندك system مرن:

- كل صفحة تختار Layout مناسب.
    
- React Query شغال على مستوى التطبيق كله.