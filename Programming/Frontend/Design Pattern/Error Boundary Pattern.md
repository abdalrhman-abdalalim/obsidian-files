#### Description:
Error boundaries are React components that catch JavaScript errors in their subtree, log them, and display fallback UIs instead of crashing the app.

#### Benefits:
- Prevents crashes by isolating errors.
- Improves user experience by displaying friendly error messages.
- Centralizes error handling for specific UI sections.

-  send fallback function and children as a props , and take state from error boundary component to check error states and use constructor to take props from component 

#### Example:
``` tsx
import { Component, ReactNode } from "react";

  

interface ErrorProps {

    fallback: ReactNode;

    children:ReactNode

}

interface ErrorState{

    isError: boolean;

    error: Error | null;

}

  

export default class ErrorBoundaryPattern extends Component<ErrorProps, ErrorState> {

  constructor(props: ErrorProps) {

    super(props);

    this.state = { isError: false, error: null };

  }

  static getDerivedStateFromError = (error: Error): ErrorState => {

    return { isError: true, error };

  };

  render(): ReactNode {

    if (this.state.isError) {

      return this.props.fallback;

    }

    return this.props.children;

  }

}

  

export const ErrorFallback = () => {

  return <div>there is an error</div>;

};








-------------------------------------------------------------------------------------

 <ErrorBoundaryPattern fallback={<ErrorFallback/>}>

	<ErrorComponet/>

  </ErrorBoundaryPattern>
```

