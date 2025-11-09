
## Animate each children sequentially 
### **🛠️ How It Works**

👉 **Step 1:** Define a **parent container** with `variants` that control all children animations.  
👉 **Step 2:** Use `staggerChildren` to make each element animate **one after the other**.  
👉 **Step 3:** Apply **opacity and y-transition** to each child (`h6`, `h1`, `p`).

``` tsx
<motion.div 
  className="reviewsSection"
  initial="hidden"
  whileInView="visible"
  viewport={{ once: true }}
  variants={{
    hidden: { opacity: 0 },
    visible: { opacity: 1, transition: { staggerChildren: 0.3 } },
  }}
>
  <motion.h6 
    variants={{
      hidden: { opacity: 0, y: 20 },
      visible: { opacity: 1, y: 0 },
    }}
  >
    Practice Advice
  </motion.h6>
  
  <motion.h1 
    variants={{
      hidden: { opacity: 0, y: 20 },
      visible: { opacity: 1, y: 0 },
    }}
  >
    Make Online Education Accessible
  </motion.h1>

  <motion.p 
    variants={{
      hidden: { opacity: 0, y: 20 },
      visible: { opacity: 1, y: 0 },
    }}
  >
    Discover what our students are saying in the Reviews section. Real feedback from learners who have benefited from our courses.
  </motion.p>
</motion.div>

```

