- #### any element written by motion.HTMLelement
- #### initial used for initial animation
- #### animate used for animation properties
- #### exit is a animation occurs when component is unmounting but it should routed by ==animatePresence==
- #### Adding `layout` to a motion component enables **automatic layout animations** when the component's position or size changes.
- #### The `mode` prop in `AnimatePresence` controls how **entering and exiting** elements are handled, especially when layout changes occur.

#### Modes Available:

1. **`sync` (default)**
    
    - The new element enters as soon as the old one exits.
    - No layout shifts are considered.
2. **`wait`**
    
    - The new element waits for the old one to **fully exit** before entering.
    - Prevents layout flickering.
3. **`popLayout`**
    
    - When an element exits, the layout shifts **before** the new one enters.
    - Helps avoid awkward resizing issues in lists or grid layouts.

``` jsx
 <div
        style={{
          backgroundColor: "red",
          height: "100vh",
          display: "flex",
          justifyContent: "center",
          alignItems: "center",
        }}
      >
        <motion.button
          onClick={() => {
            setIsVisible(!isVisible);
          }}
          layout
        >
          Click here
        </motion.button>
        <AnimatePresence mode="popLayout">
          {isVisible && (
            <motion.div
              initial={{
                rotate: "0deg",
                scale: 0,
              }}
              animate={{
                rotate: "180deg",
                scale: 1,
                y: [0, 100, -200, 0],
              }}
              transition={{
                duration: 2,
                times: [0, 0.33, 0.66, 1], // Must be within 0-1 range\
              }}
              exit={{
                rotate: "-360deg",
                scale: 0,
              }}
              style={{
                backgroundColor: "black",
                width: "200px",
                height: "200px",
                display: "flex",
                justifyContent: "center",
                alignItems: "center",
              }}
            ></motion.div>
          )}
        </AnimatePresence>
      </div>
```