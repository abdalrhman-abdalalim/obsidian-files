#### Children Component Pattern
- when you use expensive component in you component , so if you use useState it will occurs performance issues if state reRendered.
-  in this case you can assign expensive component into this component
- **Benefits :**
	- increase reusability by decoupling layout from component logic
	- promote clear separation of concerns between parent and child component
	- simplifies testing and debugging
	- Code : 
		- **Rendered Output:** 
			``` tsx
				<React.StrictMode>
					<App children={<ExpensiveComp/>} />
				</React.StrictMode> 
				// Here I assign ExpensiveComp as children in App 
				***************************************************
				let startTime = performance.now();
				while (performance.now() - startTime < 1000) {}
				   return(
					   <div>
						   <h1>Expensive Component</h1>
					   </div>
				   )
				****************************************************
				function App({Children}:{Children:ReactNode})
				const [counter, setCounter] = useState<number>(0);
				  return (
					<>
					  <h1>Your counter is {counter}</h1>
					  <button onClick={() => setCounter(counter + 1)}>increase</button>
					  <button onClick={() => setCounter(counter - 1)}>decrease</button>
					  {Children}
					</>
				 // Here take children as reactNode ans display it in my project 		```
				```




