## It is an animation library
-  you can download it in your project using cdn


### Tween
- Tween is what does all the animation work - think of it like a high-performance property setter.
- **Method for creating a Tween :**
	- gspa.to()          ----> You define the **end** values to animate _to_, GSAP uses the current values as the start values.
	- gsap.from()      ----> You define the **starting** values to animate _"from"_, GSAP uses the current values as the destinations (like a tween running backwards).
	- gsap.fromTo()  ----> It allows you to define both the initial (`from`) and final (`to`) properties of the animation
- ### Syntax of gsap 
```js
	gsap.Method(".TargetClass",{
		delay:12 , // The delay before animation should begin
		duration : 10 , // set animation duration 
		yoyo : true , // alternating backward and forward on each repeat.
		opacity : 0.4 , // the opacity of element
		x : 100 , // where the element go or come for x axios 
		y : 100 , // where the element go or come for y axios 
		repeat : -1 , // -1 is mean infinite , but you can assign number to it
		ease : "bounce" , // this value is constant and you can explore more on gsap.com
		rotation : 180 , // rotation of element
		stagger : {
			amount : 3 // if more than one element has same class , by default all of them will apply animation , but stgger will apply delay between each animate of each element
		}, 
		onStart:() => { // This animations will apply in the begining of animation
			// your animation code
		},
		onUpdate:() => {//function that should be called every time the animatio updates
			// your animation code
		},
		onComplete:()=>{//  called when the animation has completed.
			// your animation code
		}
	})
```