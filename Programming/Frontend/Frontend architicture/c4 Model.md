## C4 Model – Architecture Visualization Overview

### 🔹 What is the C4 Model?

- A series of **4 hierarchical diagrams** to visualize the architecture of a system.
    
- Developed by **Simon Brown**, software architect and author of _Software Architecture for Developers_.
    
- Described as "**Google Maps for code**" – zoom levels from big picture to fine details.
    

---

## 🔭 The 4 Levels of the C4 Model

### 1️⃣ System Context Diagram (Level 1)

- Shows the **system as a whole** within its environment.
    
- Includes:
    
    - **Primary users** (e.g., Customers, Drivers, Restaurant owners).
        
    - **External systems** (e.g., Stripe for payments, Admin system).
        
- Useful for:
    
    - **Documentation**
        
    - **Non-technical stakeholders** (PMs, executives)
        
- Stable over time; doesn’t change often.
    
- Diagrams include:
    
    - Labeled **boxes** with short descriptions.
        
    - Labeled **arrows** to remove ambiguity.
        

---

### 2️⃣ Container Diagram (Level 2)

- Zooms in on the system to show **internal containers** (apps, APIs, databases).
    
- Containers are things like:
    
    - Web/mobile applications
        
    - APIs
        
    - Databases
        
- Good for:
    
    - **Technical orientation**
        
    - Still suitable for **non-technical** audiences
        
- Might mention tech stack (e.g., React, PostgreSQL) briefly.
    
- Changes occasionally, but less frequently than code.
    

---

### 3️⃣ Component Diagram (Level 3)

- Zooms into a **specific container** to show its **internal components**.
    
- Components vary depending on the system (e.g., controllers, services, facades).
    
- In frontend projects, component diagrams are **less useful out-of-the-box**, so modifications are often needed.
    
- Aimed at **developers/architects**, not for general documentation.
    
- Draw only when:
    
    - Communicating technical changes
        
    - Writing a **design or discovery document**
        
- Not recommended to draw for every container.
    
- Cannot be easily generated automatically from code.
    

---

### 4️⃣ Code Diagrams (Level 4)

- Zooms into a component to show **actual code structure**.
    
- Examples:
    
    - UML class diagrams
        
    - ER diagrams
        
    - Custom architecture breakdowns
        
- Should be used **only when needed**, especially for communication.
    
- For frontend, code-level diagrams will be discussed later in the course.