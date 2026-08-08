# CookGraf: Intelligent Recipe & Kitchen Planning

**CookGraf** is a graph-powered recipe and kitchen-planning platform for families and home cooks. It turns the ingredients you already have into recipe recommendations, reasoned substitutions, and a ready-to-use shopping list — cutting down on food waste and on the daily "what's for dinner?" friction.

Unlike a static cookbook or recipe website, CookGraf actively plans alongside the user: it looks at what's on hand, suggests what to cook, explains what's missing, and keeps the shopping list up to date. Part of the Edniix Inova ecosystem.

---

### 👁️ The Vision

For families and hobby cooks who decide daily what to make for dinner, CookGraf works as an active planning partner rather than a passive reference. By reasoning over what's already in the kitchen, it recommends recipes that make the best use of existing ingredients, surfaces exactly what's missing, and proposes sensible substitutes before defaulting to a shopping trip.

**Product goal:** enable users to find recipes that fit their existing ingredients and automatically plan what's missing for the shop — simplifying meal planning, reducing food waste, and saving time in the kitchen.

---

### 🧠 Technical Architecture: Two Graphs, Three Services

CookGraf is built on two connected knowledge structures, exposed through independent services that communicate over APIs:

#### 1. Property Graph Service — "What exists?"
The factual backbone of the platform: recipes as data — ingredients, cooking methods, required equipment, region, cooking time. This is the structured, queryable digital cookbook that answers "what fits my ingredients?" It does not suggest substitutes and does not manage the shopping list — that's the other two services.

#### 2. Knowledge Graph Service — "What can I use instead?"
Models relationships between ingredients (e.g. similar flavor profile, similar chemistry) and between kitchen equipment (e.g. which method fits when a device is missing). This is what makes CookGraf "smart": when something's missing, it proposes a reasoned alternative — or an honest "no match" — instead of a random guess. It has no knowledge of concrete recipes; the Property Graph supplies the base ingredient or device, this service only supplies the replacement.

#### 3. Shopping List Service
Collects, consolidates, and exports what still needs to be bought: merges missing ingredients across recipes and multi-day meal plans (summing quantities, removing duplicates), tracks purchased status, and exports the result for print or mobile. It doesn't decide what's missing (Property Graph) or suggest substitutes (Knowledge Graph) — it just tracks the outcome.

```
User Input (available ingredients, equipment)
                    │
                    ▼
┌───────────────────────────────────────────────────────┐
│   CookGraf — independent services, API-driven         |
│                                                       | 
│   Property Graph ───────────>  Knowledge Graph|       |
│   (recipes & matching)        (find substitutes)      | 
│          |                                            | 
│          └──────────────────>  Shopping List          | 
│                               (missing ingredients)   |  
└───────────────────────────────────────────────────────┘
                    │
                    ▼
        Output: Recipe, Alternative, Shopping List
```

---

### 🚧 Project Status

CookGraf is currently in the specification phase. See [cookgraf/cookgraf/README.md](cookgraf/cookgraf/README.md) for the epics, feature breakdown, and per-service interface contracts that let the Property Graph, Knowledge Graph, and Shopping List services be designed and built in parallel, each against a shared contract rather than against each other.

---

**Built by Edniix Inova** — _Connecting what's in your kitchen to what's possible._
