# CookGraf — Epics, Features & Service Contracts

This document breaks the [CookGraf](../../README.md) product goal down into epics and features, and defines the fixed input/output contract for each of the three services (Property Graph, Knowledge Graph, Shopping List) so teams can build against the contract instead of blocking on one another.

---

### 📋 Epics & Features

**Epic 1 — Recipe Recommendations from Available Ingredients**
Help the user find recipes that make the best use of what's already in the kitchen.
- Enter available ingredients and get matching recipe suggestions
- Search for recipes that use as many available ingredients as possible, to minimize waste
- See exactly which ingredients a recipe is missing before deciding whether to cook it
- Filter recipes by cooking time to fit a schedule

**Epic 2 — Shopping & Kitchen Planning**
Help the user plan meals and shopping with less manual bookkeeping.
- Automatically add missing ingredients to a shopping list
- Mark shopping list items as purchased and keep track of progress
- Plan recipes across multiple days and consolidate the resulting shopping list into one
- Print the shopping list or send it to a phone for use while shopping

---

### 🔌 Service Contracts

Each service owns a fixed input/output contract, so teams can build against the contract instead of blocking on one another:

| Service | Operation | Input | Output |
|---|---|---|---|
| Property Graph | Find recipes by ingredients | List of available ingredients | Recipes ranked by match % |
| Property Graph | Find missing ingredients | Recipe ID + available ingredients | Missing ingredients, incl. required quantity |
| Property Graph | Filter by cooking time | Recipe list + time limit (e.g. "< 30 min") | Filtered recipe list |
| Knowledge Graph | Find ingredient substitute | One missing ingredient | Alternatives + reasoning (e.g. "similar fat profile"), or an honest "no match" |
| Knowledge Graph | Find equipment substitute | Missing equipment + required method | Alternative equipment + adjusted method/time + note on possible outcome changes |
| Shopping List | Add to list | Missing ingredients (from Property Graph) | Consolidated list (duplicates merged, quantities summed) |
| Shopping List | Mark as purchased | List entry + "purchased" status | Updated entry status |
| Shopping List | Consolidate weekly plan | Selected recipes per day | Merged list across all days |
| Shopping List | Export | Finished list | Export format (print view, text message, etc.) |

> Ground rule: if a story needs input from another service, take the contract above as given and build against it — don't wait on the other team.
