
1. **Next.js:**
    
    - In Next.js, you can **import images directly** using the `import` statement, making it easy to use them in your components.
    - Example:
        ```js
        import logo from './assets/logo.png'; <Image src={logo} alt="Logo" />
```
        
1. **React:**
    
    - In React, images are imported as objects. To use them as a source, you'll need to reference the `.src` property.
    - Example:
        ```tsx
        import logo from './assets/logo.png'; <img src={logo.src} alt="Logo" />
```
        
1. **Image Component in Next.js:**
    
    - **Lazy Loading**: The `<Image />` component in Next.js automatically supports lazy loading, which means images are loaded only when they come into view, optimizing performance and reducing initial page load time.
        - This is especially beneficial for large images or images placed further down the page.
    - **WebP Format**: The WebP image format is recommended because it offers better **compression**, **quality**, and **smaller file sizes** compared to formats like PNG and JPEG.
        - Next.js’s `<Image />` component automatically serves WebP images when supported by the browser.
        - Example:
            
        ```tsx
    <Image src="/image.webp" alt="Image in WebP format" width={500} height={300} />
        
```    
            
    - **Image Priority**: You can use the `priority` attribute to ensure that specific images, like hero images or above-the-fold content, are loaded as a **priority**.
        - This tells the browser that the image should be visible **immediately** for a better user experience and reduced perceived loading time.
        - Example:
	        ```tsx
 <Image src="/hero-image.webp" alt="Hero Image" width={1200} height={800} priority />
      
```
            
