## First Principles Thinking in Software Development

First principles thinking means **breaking down a problem to its most fundamental truths** and reasoning up from there — rather than reasoning by analogy ("we do it this way because others do it this way").

Coined by Aristotle, popularized in engineering by Elon Musk.

---

### The Core Process

```
1. Identify and challenge assumptions
2. Break the problem down to fundamental truths
3. Rebuild the solution from scratch using those truths
```

---

### Applied to Software

#### ❌ Analogy Thinking (what most devs do)
> "We use a REST API because that's the standard."
> "We use Redux because every React app uses it."
> "We use microservices because Netflix does."

#### ✅ First Principles Thinking
> "What does our UI actually need from the server? Just one domain's daily totals on popup open."
> "Do we actually need global state? We have 2 components reading 1 data source."
> "Is the complexity of distributed services justified for our user count?"

---

### Practical Examples

| Situation | Analogy Approach | First Principles Approach |
|-----------|-----------------|--------------------------|
| **State management** | "Use Redux, it scales" | "What state needs to be shared? Who reads it? — `chrome.storage` + a hook is sufficient" |
| **API design** | "Use REST with CRUD endpoints" | "What queries does the UI actually make? Design the data shape around read patterns" |
| **Performance** | "Add a cache layer" | "Why is it slow? — profiling reveals it's a re-render, not a fetch" |
| **Database choice** | "Use PostgreSQL, it's reliable" | "What are my access patterns? Key-value daily aggregates + append-only logs → `chrome.storage` + IndexedDB fits exactly" |
| **Framework choice** | "Everyone uses Next.js" | "Do we need SSR? SEO? No — it's a browser extension popup. Vite + React is the right size" |

---

### The 5 Questions Framework

When tackling any engineering decision, ask in order:

1. **What problem are we actually solving?** (not the assumed problem)
2. **What do we know for certain?** (constraints, invariants — e.g. MV3 service workers are ephemeral)
3. **What are we assuming?** (challenge every one)
4. **What's the simplest solution that satisfies the real constraints?**
5. **What would make this solution wrong?** (stress-test it)

---

### In This Project (Do Little)

Every design decision in design.md is a first-principles outcome:

- **Why 4 storage tiers?** Because each tier has fundamentally different characteristics (speed, capacity, persistence, sync) and different data has different access patterns — not because "tiered storage is best practice"
- **Why WXT over Plasmo/webpack?** Because the fundamental requirement is MV3 + Chrome + Edge + fast iteration — WXT is the minimal tool that satisfies exactly that
- **Why no Redux?** The popup reads from `chrome.storage`. There's no cross-component state problem to solve
- **Why Rust for native companion?** The fundamental requirement is OS-level process enumeration with minimal memory footprint and no runtime dependency — Rust satisfies all three

---

> **The key habit:** Every time you reach for a tool, pattern, or library — ask *"what problem does this solve?"* and *"does that problem actually exist here?"*