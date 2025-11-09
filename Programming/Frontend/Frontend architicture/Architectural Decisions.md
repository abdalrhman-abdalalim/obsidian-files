## Architectural Decisions Summary

- **Architectural Decisions** are decisions that affect the system's structure, are hard to change later, or have long-term impact (e.g., choosing a frontend framework, repo structure, third-party services).
- In early project stages, most decisions are architectural because design-level details (code, UI) are not clear yet.
- Examples:
  - Choosing between Next.js, Remix, Nuxt, etc.
  - Deciding repo structure (monorepo vs multi-repo).
  - Choosing third-party services for specific requirements (e.g., Pusher for real-time features).
  - Planning code organization (Domain-Driven Design, Clean Architecture, etc.).
  - Planning observability & monitoring strategies early if reliability is a key quality.

### Key Principles:

1. **Don't rush to decide everything early.** Use "Last Responsible Moment" to decide when you have enough info.
2. **Document WHY, not just WHAT.** The reasoning behind the decision is more important than the decision itself.

### Architectural Decision Records (ADRs):

- ADRs are small documents that log important architectural decisions.
- Simple ADR template includes:
  - Title & ID
  - Status (Draft, Accepted, etc.)
  - Context (why the decision is needed)
  - Decision (what was decided)
  - Consequences (positive and negative)
- ADRs build an "Architectural Decision Log" that tells the story of how & why architecture evolved.

### Example ADR Summary:

- **Decision**: Use Next.js for frontend.
- **Context**: Need a robust, scalable framework within a tight 4-month deadline. Team already experienced with Next.js.
- **Consequences**:
  - Positive: Fast development, known ecosystem, flexibility.
  - Negative: Tied to Next.js constraints, potential scalability considerations.