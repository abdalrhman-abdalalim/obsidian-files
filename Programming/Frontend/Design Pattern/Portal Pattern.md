#### Description:
Portals allow rendering children into a DOM node outside of the parent component's DOM hierarchy, while preserving React's context.

#### Benefits:
- Useful for modals, tooltips, and dropdowns that need to escape parent CSS constraints.
- Improves accessibility by rendering directly into the document body.
- Retains component's internal state and context.

#### Example in Real Tools:
- **Material-UI Dialog:** Uses portals for modals to render them outside the main DOM tree.

``` tsx 
import { ReactNode, useEffect } from "react";
import { createPortal } from "react-dom";
interface IProps {
    isOpen: boolean;
    handleClose: () => void;
    children: ReactNode;
}
const Modal = ({ isOpen, handleClose, children }: IProps) => {
    const modalRoot = document.getElementById("root") as HTMLDivElement;
    const modalElement = document.createElement("div") as HTMLDivElement;
    useEffect(() => {
        if (modalRoot) {
            modalRoot.appendChild(modalElement);
        }
        return () => {
            modalRoot.removeChild(modalElement);
        }
    }, [modalElement, modalRoot])
    
    if (!isOpen) return null;
    return createPortal(
      <div
        style={{
          position: "fixed",
          inset: 0,
          background: "aqua",
          display: "flex",
          flexDirection: "column",
          placeItems: "center",
          justifyContent: "center",
        }}
      >
        <div>{children}</div>
        <div>
          <button onClick={handleClose}>close modal</button>
        </div>
      </div>,modalElement
    );
}
export default Modal;
```

`createPortal`: A React function that allows rendering children into a DOM node that exists outside the DOM hierarchy of the parent component.

**purpose of useEffect** 
**Purpose**: Ensures that the `modalElement` is added to the DOM when the component mounts and removed when it unmounts.

- `modalRoot.appendChild(modalElement)`: Adds the newly created `modalElement` to the `root` element when the component is rendered.
- `modalRoot.removeChild(modalElement)`: Removes the `modalElement` to prevent memory leaks or stale elements in the DOM.
