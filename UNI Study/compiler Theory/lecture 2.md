
#### **phases of compiler**
##### Lexical Analysis
- scan source code into meaningful lexemes.
- The purpose of lexical analysis is that it aims to read the input code and break it down into meaningful elements called ****tokens****
- lexical analyzer represent lexemes into form of tokens : <Token-name , attribute-Value>
- called linear analysis
- ###### Lexical Analyzer 
	- if it found a token invalid it generates error
	- work closely with syntax analyzer
	- reads characters from the source code and checks for legal tokens and passes data to syntax analyzer  
	- ##### Interaction between lexical analyzer and parser :
		-  source code -> [lexical analyzer] (Token) <-----> (getNextToken) [syntax analyzer] 
	- once receiving getNextToken command from syntax analyzer the lexical analyzer reads input chars unit it can identify the next Token.
	- it could make secondary tasks : 
		- remove white spaces and newline and blanks 
		- relate error message from the compiler with source code 
	- **Token** :- is a group of chars have a collective meaning , smallest unit of meaningful data; it may be an identifier, keyword, operator, or symbol.
	- **lexeme** :- actual char sequence forming a specific token such as (num)
	- **Pattern** :- rule describing the strings associated with a token , Expressed as [Regular expression] and explaining how a particular token could be formed. 
	- ### Example about tokens :-
		 `int value =100 ;`  ---> contains the tokens :
		 <int, keyword> <value, identifier> < =, operator > <100, constant> <; , symbol>
	- #### Different Types of Tokens :-
		- **Keywords** : -  words reserved for a particular purposes and mean a special meaning to the compilers , must not used for naming a variables .
		-  **Identifier** : -  name given to various component , used for naming variable , functions , etc.. , keywords can't be identifier
		-  **Operations** : -  used to express operations in programming language
		-  **Punctuations** : -  are special symbols used to separate different code elements in PL , such as ; in C++
		-  **Strings** : -  finite streams of chars , it could be digits or chars and also could be empty string like ε
	- #### Specifications of Tokens :- 
		- #### Language 
			- language consider as a finite set of strings 
			- Computer language is set of finite sets and mathematically set of operations can be performed on them 
		- #### Regular Expressions
			- Lexical analyzer must valid finite set of valid string/tokens/lexemes that belong to language.
			- Regular expression can express finite language by defining a pattern for finite strings of symbols. 
			- grammar defined regular expression called regular grammar 
			- language defined by regular expression called regular language 
##### Syntax Analysis
- called Syntax analysis or parsing
- Take generated tokens from lexical analysis as input and generate syntax/parsing tree 
- Token arrangement are checked against source code grammar 
- Parser checks if expression is syntactically correct.
##### Semantic Analysis
- check if pares tree constructed follows language rules.
- semantic analyzer produces annotated syntax tree as output
- check if you add integer to string
##### Intermediate code generation
- generate intermediate code for the target machine
- It is between high level language and low level language 
- easier to translate into target machine code
##### Code Optimization
- optimize intermediate code 
- remove unnecessary code lines and arranges sequence of statements to speed up execution time and save CPU resources.
##### Code Generation
- takes optimized code and maps it into target machine code 
- sequence of instructions of machine code performs the task as the intermediate code would do.
##### Symbol Table
- data structure maintained throughout all phases 
- all identifiers names stored here 
- it makes it easier for compiler to quickly search the identifier.
- also used in scope management 
