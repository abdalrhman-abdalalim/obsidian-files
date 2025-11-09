### Parser : phase of compiler takes tokens as input and convert it to Intermediate Representation (IR) using existing grammar , and it also known as Syntax Analyzer.

### Parser -> ( Top Down Parser) ---- (Bottom-up Parser)
##### Top-down parser -> (Recursive descent parser) ---- (LL1 / Non recursive descent parser)
##### bottom-up parser -> (LR Parser) --- (Operator precedence parser)
##### LR parser -> (LR0) --- (SLR1) --- (LALR1) --- (CLR1)


> Note : small chars are non-terminal , and upper chars are terminal
## Top - down parser :-
- generate parse from the given input with the help of grammar productions by expanding the non-terminals. 
- It starts from start symbol and ends on the terminals.
- uses leftmost derivation.
- The input is recursively parsed for preparing a parse tree .
- may use backtracking or not 
#### -> recursive parser :- 
- also known as backtracking parser. 
- generate parse tree using backtracking
#### -> non-recursive parser :-
- know as  :
	- LL1
	- predictive parser 
	- without backtracking parser
	- dynamic parser
- use backtracking for creating parse tree
#### -> Predictive parser (LL Parser)
- similar to recursive descent parsing but without backtracking.
- can implemented using stack 
- has following component :- 
	- **Input Buffer** is string to be parsed followed by an end marker $ to donate the end of the string
	- contains combination of grammar symbols with $ on the end of the stack 
- Types of Top-down Parsing :-
	- parsing table : 2 dimensional array contains [A,a] (A for non-Terminal and 'a' for Terminal )
	- parsing program : performs some actions by comparing current element of the stack with the current input of input symbol to be read on the input buffer
	- parsing program makes some action depend on the top of the stack and the current input symbol .
## Bottom - up parser :-
- generate parse from the given input with the help of grammar productions by compressing the terminals.
- starts from terminals and end on the start symbol .
- uses right most derivation
- There are 2 types : LR , Operator precedence parser.
####  -> LR parser :-
- generate parse tree using unambiguous grammar. 
- follows rightmost derivation 
- Types : (LR0 , SLR1 , LALR1 , CLR1)
####  -> Operator Precedence Parser :-
- used for parsing programming languages with defined precedence(order of important) for operators.
- to handle different mathematical and programming expressions involving operators with different precedence levels
##### Characteristics of the operator precedence :-
1) Operator precedence -> use rules to determine the precedence between different expressions 
2) Associativity Rules : binary operators are left-associative , while exponentiation are right-associative 
3) No overlapping Operators : there must no be overlapping between operators 
#### How the operator precedence parser works ? 
- scanning the expression from left to right
- using precedence table to determine which operator to evaluate first 
- Evaluating operations on operators and numbers according to precedence and associativity
- building the expression step by step until reaching the final result

- operator precedence parser used often in programming languages that contain mathematical expression like C , Python
### Backtracking : -
- parse tree started from root node and the input string is matched against the production rules for replacing them .
- if derivation of a production fails , the syntax analyzer restarts the process using different rules of the same production
- Limitations of backtracking where if you have grammar has more number of alternatives , the cost of backtracking will be high
