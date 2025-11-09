
#### computer processing system : 
- tools and operations used to convert code written with programming language into code computer can directly understand and excute.
#### compiler :
-  computer program helps to convert High Level Language into Low level language (machine code)
- ==phases of converting HLL into LLL== 
	- **compiler** convert it into assembly language
	- **assembler** translates it into machine code
	- **linker** links all parts of program together
	- **loader** loads it into memory and excute program
#### Language processing system :
- ##### preprocessor 
	- a source program my be divided into separated files. The task of collecting source code entrusted to separate program called preprocessor .
- ##### interpreter
	- is like compiler , but compiler reads whole program , but interpreter read statement by statement and converts it to an intermediate code , excute it and then takes the next statement , if an error occurs , an interpreter stops execution and reports it.
- ##### Assembler
	- translate assembly language program into machine code  , its output called ==object file== -> contains combination of machine code instruction and the data required.
- ##### linker
	- computer program links and merge various object together to make an executable file , all these file compiled by different assembler , the major take of linker to search and locate referenced modules in a program and to determine the memory location where these codes will be loaded. 
- ##### hybrid compiler
	- a type of compiler that combines the features of compiler & interpreter . Translate human-readable source code to an intermediate byte code for later interpretation known as **JIT** (Just In Time).
- ##### source to source compiler
	- translates source code from one programming language to another programming language


### compiler could be divided according to way they output :
1) **Direct**: translate direct to machine code
2) **Translator**: use intermediate code 

- Compiler can divided into 2 phases based on the way the compile :
	- **Analysis phase** :
		- frontend phase of compiler 
		- reads source program , divide it into core parts , checks for lexical , grammar and syntax errors
		- generated an intermediate representation of the source program and symbol table  
	 - **Synthesis phase** :
		 - backend phase
		 - generate target program from intermediate source code 
- **phase** -> stage take input from previous stage & process and generate output that can used for next stage  