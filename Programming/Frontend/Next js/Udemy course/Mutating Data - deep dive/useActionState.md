`useActionState` is a Hook that allows you to update state based on the result of a form action.

###### `const [state, formAction, isPending] = useActionState(fn, initialState, permalink?);`

### `useActionState(action, initialState, permalink?)` [](https://react.dev/reference/react/useActionState#useactionstate "Link for this heading")

Call `useActionState` at the top level of your component to create component state that is updated [when a form action is invoked](https://react.dev/reference/react-dom/components/form). You pass `useActionState` an existing form action function as well as an initial state, and it returns a new action that you use in your form, along with the latest form state and whether the Action is still pending. The latest form state is also passed to the function that you provided.

```tsx
import { useActionState } from "react";  
async function increment(previousState, formData) {  
	return previousState + 1;  
}  

function StatefulForm({}) {  
	const [state, formAction] = useActionState(increment, 0);  
	return (  
		<form>  
			{state}  
			<button formAction={formAction}>Increment</button>  
		</form>  
	) 
}
```

#### Parameters 

- `fn`: The function to be called when the form is submitted or button pressed. When the function is called, it will receive the previous state of the form (initially the `initialState` that you pass, subsequently its previous return value) as its initial argument, followed by the arguments that a form action normally receives.
- `initialState`: The value you want the state to be initially. It can be any serializable value. This argument is ignored after the action is first invoked.
- **optional** `permalink`: A string containing the unique page URL that this form modifies. For use on pages with dynamic content (eg: feeds) in conjunction with progressive enhancement: if `fn` is a [server function](https://react.dev/reference/rsc/server-functions) and the form is submitted before the JavaScript bundle loads, the browser will navigate to the specified permalink URL, rather than the current page’s URL. Ensure that the same form component is rendered on the destination page (including the same action `fn` and `permalink`) so that React knows how to pass the state through. Once the form has been hydrated, this parameter has no effect.

#### Returns
`useActionState` returns an array with the following values:

1. The current state. During the first render, it will match the `initialState` you have passed. After the action is invoked, it will match the value returned by the action.
2. A new action that you can pass as the `action` prop to your `form` component or `formAction` prop to any `button` component within the form. The action can also be called manually within [`startTransition`](https://react.dev/reference/react/startTransition).
3. The `isPending` flag that tells you whether there is a pending Transition.