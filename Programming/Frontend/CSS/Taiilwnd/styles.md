==tracking-widest== : Applies letter-spacing (`0.15rem`).
==bg-gradient-to-r from-[#f9572a] to-[#ff9b05]==: Creates the gradient background.
==text-transparent==: Makes the text color transparent, revealing the gradient.

### **Breakdown of Tailwind Classes:**

| **CSS Property**                                        | **Tailwind Equivalent**                                          | **Explanation**                                              |
| ------------------------------------------------------- | ---------------------------------------------------------------- | ------------------------------------------------------------ |
| `background: linear-gradient(90deg, #ff8a05, #f9b331);` | `hover:bg-gradient-to-r hover:from-[#ff8a05] hover:to-[#f9b331]` | Creates the gradient background on hover.                    |
| `background-clip: text;`                                | `hover:bg-clip-text`                                             | Ensures the gradient is applied only to the text.            |
| `-webkit-text-fill-color: transparent;`                 | `hover:text-transparent`                                         | Makes the text color transparent so the gradient is visible. |
| `text-shadow: 0 0 18px rgba(248, 190, 42, 0.8);`        | `hover:[text-shadow:0_0_18px_rgba(248,190,42,0.8)]`              | Adds a glow effect using Tailwind’s arbitrary values.        |

