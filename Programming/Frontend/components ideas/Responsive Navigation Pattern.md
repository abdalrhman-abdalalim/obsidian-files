### ✅ **Responsive Navigation Pattern**

#### 📱 **في الموبايل (Mobile):**

- استخدم **Expandable Accordion** بدل Dropdown.
    
- ✅ يظهر تحت العنصر مباشرة في نفس الـ DOM.
    
- ❌ ما تستخدمش Portal (زي Radix `DropdownMenu`).
    
- ✅ سهل التحكم فيه باستخدام `useState`.
    

**Pattern Example:**

```tsx
<button onClick={() => setOpen(!open)}>...</button>
{open && (
  <div className="pl-4">
    {/* subCategories */}
  </div>
)}

```
---

#### 🖥️ **في الديسكتوب (Desktop):**

- استخدم **Dropdown/Popover UI** (زي Radix Dropdown).
    
- ✅ Portal مناسب هنا.
    
- ✅ يدعم Hover + Keyboard Navigation.
    
- يفضل استخدام `onMouseEnter / onMouseLeave` لفتح/غلق القائمة.
    

**Pattern Example:**

```tsx
<DropdownMenu open={open} onOpenChange={setOpen}>
  <DropdownMenuTrigger>...</DropdownMenuTrigger>
  <DropdownMenuContent>...</DropdownMenuContent>
</DropdownMenu>

```


---

### 💡 **قاعدة ذهبية تحفظها:**

> ❝ الموبايل يحب البساطة، والديسكتوب يحب القوة. ❞
> 
> استخدم **accordion في الموبايل** و **dropdown في الديسكتوب**.


```tsx
"use client";

import {

  DropdownMenu,

  DropdownMenuContent,

  DropdownMenuItem,

  DropdownMenuSub,

  DropdownMenuSubContent,

  DropdownMenuSubTrigger,

  DropdownMenuTrigger,

} from "@/components/ui/dropdown-menu";

import { cn } from "@/lib/utils";

import { ChevronDown } from "lucide-react";

import Link from "next/link";

import { usePathname } from "next/navigation";

import { useRef, useState } from "react";

  

interface MenuLinkProps {

  item: {

    id: number;

    label: string;

    href: string;

  };

  className?: string;

  activeClassName?: string;

  mobile?: boolean;

}

  

export const MenuLink = ({

  item,

  className = "",

  activeClassName = "",

  mobile = false,

}: MenuLinkProps) => {

  const pathname = usePathname();

  const isActive =

    pathname === item.href || (pathname === "/" && item.href === "/");

  

  return (

    <Link

      href={item.href}

      className={cn(

        className,

        "transition-colors",

        mobile

          ? "block w-full py-3 px-5 rounded-lg text-[15px] hover:bg-[var(--secondary)] text-[var(--foreground)]"

          : "py-2 px-4 rounded-md hover:bg-[var(--secondary)] text-[var(--foreground)]",

        isActive &&

          "bg-[var(--secondary)] font-semibold text-[var(--foreground)] rounded-md"

      )}

    >

      {item.label}

    </Link>

  );

};

  

const CategoryMenuItem = ({

  item,

  mobile = false,

}: {

  item: any;

  mobile?: boolean;

}) => {

  const hasSubCategories = item.subCategories?.length > 0;

  const [open, setOpen] = useState(false);

  const triggerRef = useRef<HTMLButtonElement>(null);

  const [isHovering, setIsHovering] = useState(false);

  

  const handleMouseEnter = () => {

    setIsHovering(true);

    if (hasSubCategories && triggerRef.current && !mobile) {

      triggerRef.current.click();

    }

  };

  

  const handleMouseLeave = () => {

    setIsHovering(false);

  };

  

  return (

    <div

      className={`relative ${mobile ? "w-full" : ""}`}

      onMouseOver={!mobile ? handleMouseEnter : undefined}

      onMouseOut={!mobile ? handleMouseLeave : undefined}

    >

      {mobile ? (

        <div className="w-full">

          <button

            onClick={() => setOpen((prev) => !prev)}

            className="w-full flex justify-between items-center p-3 rounded-lg text-left text-[var(--foreground)] hover:bg-[var(--secondary)]"

          >

            {item.label}

            {hasSubCategories && (

              <ChevronDown

                className={`h-4 w-4 transition-transform duration-200 ${

                  open ? "rotate-180" : ""

                }`}

              />

            )}

          </button>

          {hasSubCategories && open && (

            <div className="pl-4 mt-2 space-y-2">

              {item.subCategories.map((subItem: any) => (

                <div key={subItem.id}>

                  {subItem.subCategories?.length ? (

                    <details className="group">

                      <summary className="flex justify-between items-center p-3 rounded-lg cursor-pointer hover:bg-[var(--secondary)]">

                        <span className="text-[var(--foreground)]">

                          {subItem.label}

                        </span>

                        <ChevronDown className="h-4 w-4 transition-transform duration-200 group-open:rotate-180" />

                      </summary>

                      <div className="ml-4 mt-1 space-y-1">

                        {subItem.subCategories.map((subSubItem: any) => (

                          <MenuLink

                            key={subSubItem.id}

                            item={subSubItem}

                            mobile

                            className="block py-2 px-4 hover:bg-[var(--secondary)] rounded-md"

                          />

                        ))}

                      </div>

                    </details>

                  ) : (

                    <MenuLink item={subItem} mobile />

                  )}

                </div>

              ))}

            </div>

          )}

        </div>

      ) : (

        <DropdownMenu open={open} onOpenChange={setOpen}>

          <DropdownMenuTrigger asChild>

            <div className="flex items-center gap-1 cursor-pointer group rounded-md hover:bg-[var(--secondary)] transition-colors text-[var(--foreground)]">

              <button

                ref={triggerRef}

                className={cn(

                  "text-sm transition-colors flex items-center px-3 py-2 rounded-md font-medium hover:bg-[var(--secondary)] text-[var(--foreground)]",

                  hasSubCategories ? "gap-1" : ""

                )}

              >

                {item.label}

                {hasSubCategories && (

                  <ChevronDown

                    className={`h-4 w-4 transition-transform duration-200 ease-out ${

                      open ? "rotate-180" : ""

                    }`}

                  />

                )}

              </button>

            </div>

          </DropdownMenuTrigger>

  

          {hasSubCategories && (

            <DropdownMenuContent

              className="min-w-[250px] bg-[var(--background)] text-[var(--foreground)] rounded-lg border border-[var(--secondary)]/20 p-3 shadow-lg"

              align="start"

              sideOffset={5}

              avoidCollisions={true}

            >

              {item.subCategories.map((subItem: any) => (

                <div key={subItem.id}>

                  {subItem.subCategories?.length ? (

                    <DropdownMenuSub>

                      <DropdownMenuSubTrigger className="flex justify-between w-full p-3 text-sm rounded-lg hover:bg-[var(--secondary)] transition-colors duration-150 text-[var(--foreground)]">

                        {subItem.label}

                      </DropdownMenuSubTrigger>

                      <DropdownMenuSubContent className="min-w-[200px] bg-[var(--background)] text-[var(--foreground)] rounded-lg border border-[var(--foreground)]/20 p-3 ml-1 shadow-lg">

                        {subItem.subCategories.map((subSubItem: any) => (

                          <DropdownMenuItem key={subSubItem.id} asChild>

                            <MenuLink

                              item={subSubItem}

                              className="hover:bg-[var(--secondary)] w-full p-3 rounded-lg transition-colors duration-150 text-[var(--foreground)]"

                            />

                          </DropdownMenuItem>

                        ))}

                      </DropdownMenuSubContent>

                    </DropdownMenuSub>

                  ) : (

                    <DropdownMenuItem asChild>

                      <MenuLink

                        item={subItem}

                        className="hover:bg-[var(--secondary)] w-full p-3 rounded-lg transition-colors duration-150 text-[var(--foreground)]"

                      />

                    </DropdownMenuItem>

                  )}

                </div>

              ))}

            </DropdownMenuContent>

          )}

        </DropdownMenu>

      )}

    </div>

  );

};

  

export default CategoryMenuItem;
```