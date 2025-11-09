
## **Next issue**

### <font color="red">Problem</font>  : 
node:internal/modules/cjs/loader:1228
  throw err;
  ^

Error: Cannot find module 'D:\Projects\next\dist\bin\next'
    at Function._resolveFilename (node:internal/modules/cjs/loader:1225:15)
    at Function._load (node:internal/modules/cjs/loader:1055:27)
    at TracingChannel.traceSync (node:diagnostics_channel:322:14)
    at wrapModuleLoad (node:internal/modules/cjs/loader:220:24)
    at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:170:5)
    at node:internal/main/run_main_module:36:49 {
  code: 'MODULE_NOT_FOUND',
  requireStack: []
}   

### <font color="green">Solve</font>  : 

 yarn add cjs-loader --save




---

## **Next issue**

### <font color="red">Problem</font>  : 
Type error: Type '{ params: { id: string; }; }' does not satisfy the constraint 'PageProps'. Types of property 'params' are incompatible. Type '{ id: string; }' is missing the following properties from type 'Promise': then, catch, finally, [Symbol.toStringTag]

### <font color="green">Solve</font>  : 

**`npx @next/codemod@latest next-async-request-api` .**

```
type tParams = Promise<{ slug: string[] }>;

export default async function Challenge({ params }: { params: tParams }) {
  const { slug } = await params;
  const productID = slug[1];
}
```


 ---
##  **js-cookie issue**

### <font color="red">Problem</font>  : 
Could not find a declaration file for module 'js-cookie'. 'd:/Projects/React & Next Projects/Code Spark/Code-Spark/code-sparks/node_modules/js-cookie/dist/js.cookie.mjs' implicitly has an 'any' type.
  Try `npm i --save-dev @types/js-cookie` if it exists or add a new declaration (.d.ts) file containing `declare module 'js-cookie';`

### <font color="green">Solve</font>  : 

**`npm install --save-dev @types/js-cookie` .**



