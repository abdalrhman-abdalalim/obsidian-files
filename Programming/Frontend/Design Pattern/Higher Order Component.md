
### Description : 
A higher-order component is a function that takes a component as a n argument and returns a new enhanced component by injectional props or behavior

### Benefits :
- Enables reusability of logic across components
- Enhance components without modifying their source code  
- Support separation of concerns by wrapping components


-> I will make a function and make it allow to take component as a props and each component passed to it , add to it styles or any thing you want 

### Example
``` tsx
import { ButtonHTMLAttributes } from "react";
import WithStyles from "./WithStyles";
interface IProps {
    props : ButtonHTMLAttributes<HTMLButtonElement>
} 
const Button = ({props}:IProps) => {
   return(
       <button type="button" style={{padding:10,margin:10}} {...props}>click here</button>
   )
}
export const StyledButton = WithStyles(Button);
```

**Here I pass Button component into WithStyles component which accept component as a style**


``` tsx
import { ComponentType, CSSProperties } from "react";
const WithStyles = <P extends object>(Component: ComponentType<P>) => {
    return (props: P) => {
        const style: CSSProperties = { padding: 10, margin: 10 };
        return <Component style={style} {...props} />
   }
}
export default WithStyles;
```

**Here I give WithStyles props - Generic Type `P`:**
    - Represents the specific props expected by the wrapped `Component`.
- **Type Checking:**
    - If you pass invalid props to the wrapped component, TypeScript will throw an error.