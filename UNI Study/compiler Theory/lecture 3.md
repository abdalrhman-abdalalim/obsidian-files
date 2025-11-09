
- ##### Syntax Definition :- 
	- if ( expression ) statement else statement ->common way to control the flow of a program
	- This means that if a certain condition (the expression) is true, one block of code (the first statement) will execute. If the condition is false, another block of code (the second statement) will run instead.
	- Then article translate this programming concept into a formal grammar rule : 
		`stmt → if (expr) stmt else stmt`. 
		arrow means "can have the form"
	- Terminal and non-Terminal : 
		- Terminal : are the actual chars or strings used in code (If - else - parentheses) , They are the fixed elements that don't change
		- non-Terminal : patterns can be replaced ,  [expr]-[stmt] they can represent a variety of actual expressions or statement depending on the specific program or context .
- ##### Definition of grammars :-
	- context free grammar has 4 components : 
		1) set of terminal symbols , sometimes refers as tokens 
		2) set of non terminal symbols , sometimes called syntactic variables.
		3) set of production , where each production consists of non-terminal. (أي سهم على يمينيه حاجه وعلى شماله حاجه ) ------> Left side of production called head || Right side of production called body
		4) make one non-terminal as the start symbol
- ##### Derivations :-
	- beginning with the start symbol and repeatedly replacing non terminal with one of the body of the productions 
	- List -> List + digit -> List - digit + digit -> digit - digit + digit -> 9 + 5 - 2 
- #### Parse Tress :-
	- pictorially shows how the start symbol of a grammar derives a string in the language.
								    ==List
								(List)   (+)     (digit)==
	-  parse tree according to the grammar is a tree with following properties :-
		- the root is labeled by start symbol 
		- each leaf is labeled by terminal or ↋
		- each interior node is labeled by a non terminal
	- if A -> ↋ then node labeled A may have a single child labeled ↋.
- #### Ambiguity :-
	- grammar that have more than one parse tree
- #### Associativity of Operators :-
	-  By convention, 9+5+2 is equivalent to (9+5)+2 and 9-5-2 is equivalent to (9-5)-2.
- #### Precedence of Operators :-
	- Rules defining the relative precedence of operators are needed when more than one kind of operator is present
	- Keywords allow us to recognize statements since most statements begin with a keyword or a special character.