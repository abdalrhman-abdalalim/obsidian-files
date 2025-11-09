Architectural Drivers are **factors that influence the architecture** of a system. They shape **architectural requirements** (success criteria) and lead to **architectural decisions** (high-level system choices).

---

### 📌 Main Architectural Drivers:

1. **Business Goals**:
    
    - The primary reason why the system is being built.
        
    - Examples: Increase revenue, reduce cost, improve velocity, reduce tech debt.
        
    - If unmet, the architecture is not successful.
        
2. **Quality Attributes (Architectural Characteristics)**:
    
    - The "ilities" (e.g., scalability, maintainability, reliability, security, performance).
        
    - Focus on the most influential ones.
        
    - There’s always a baseline level expected for each.
        
3. **Constraints**:
    
    - **Technical Constraints**: Predefined tech stack (e.g., must use Angular).
        
    - **Business Constraints**: Budget limits, strict deadlines.
        
    - Non-negotiable and limit scope (decisions already made).
        
4. **Functional Requirements**:
    
    - System’s features & capabilities (e.g., search items, add to cart, login).
        
    - Not all functional requirements influence architecture — focus on **Architecturally Significant Requirements (ASRs)**.
        
5. **Team’s Experience & Knowledge**:
    
    - Skillset of the development team and architect impacts tech choices and design patterns.
        
    - Broader experience leads to better decision-making.
        
6. **Technology Trends**:
    
    - Stay updated with new trends but prefer "boring/stable" technologies for core architecture.
        
    - Evaluate trade-offs before adopting new tech.
        

---

### Flow of Influence:

**Architectural Drivers → Architectural Requirements → Architectural Decisions**

---

### Notes:

- The **same app can have completely different architectures** due to differing drivers.
    
- Constraints help narrow scope and simplify decision-making.
    
- Architect’s job is to evaluate which drivers are **significant and influential**.