
## **Js Engine :**
- ####  translate js code into something the computer can understand and excute
- #### most popular one is V8 (google chrome) , spiderMonkey (Firefox) , JavaScript Core (Safari)

## **Stages of compiling JS code**
- #### js code  -> parser -> Abstract Syntax Tree (AST) -> interpreter -> compiler
- ##### parser 
	- cuts code into meaningful tokens
- ##### AST 
	- An **AST (Abstract Syntax Tree)** is like a map of your code. It takes your source code and breaks it down into a tree-like structure that makes it easier for the computer to understand and process.
- ##### Interpreter
	- compile code line by line 
	- it was slow and simple
- ##### Compiler 
	- compile all the code 
	- it was fast but complex

### Js used JIT compiler 
- It merge between compiler and interpreter
- create optimized code 
- process in which code is translated from an intermediate representation or a higher-level language into machine code  at runtime 
- JIT compilers typically continuously analyze the code as it is executed, identifying parts of the code that are executed frequently (hot spots). If the speedup gains outweigh the compilation overhead, then the JIT compilers will compile those parts into machine code. The compiled code is then executed directly by the processor, which can result in significant performance improvements.
- if I have 2 objects with different names but body is similar , it creates optimized code