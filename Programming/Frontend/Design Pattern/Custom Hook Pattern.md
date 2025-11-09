#### Description 
encapsulate reusable logic in custom hooks, making it possible to share stateful logic across components without duplicating code.

#### Benefits 
-  Makes stateful logic reusable and testable
- Improves readability by reducing clutter  in component files.
- Adheres to to the DRY (Don't Repeat Yourself) principle

#### Example 
``` tsx
	import { useUserProfile } from "./useUserProfile";

  

const UserProfile = () =>{

    const {isActive,isOnline} = useUserProfile();

   return (

     <div>

       <span>{isOnline ? "Online" : "offline"}</span>

       <span>{isActive&&!isOnline ? isActive.toLocaleString() : ""}</span>

     </div>

   );

}

  

export default UserProfile; 


--------------------------------------------------------------------------------------

// This is created custom hook

import { useState, useEffect } from "react"

  

export const useUserProfile = () => {

    const [isOnline, setIsOnline] = useState<boolean>(false);

    const [isActive, setIsActive] = useState<Date | null>(null);

    useEffect(() => {

      const checkOnline = () => {

        const statue = Math.random() > 0.5;

        setIsOnline(statue);

        if (!statue) {

          setIsActive(new Date());

          setIsOnline(false);

        }

      };

      const interval = setInterval(checkOnline, 3000);

      return () => clearInterval(interval);

    });

    return {isOnline,isActive}

}
```