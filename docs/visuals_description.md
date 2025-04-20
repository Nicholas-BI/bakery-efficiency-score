# 🎨 Visuals Overview

This single-page Power BI report helps *Bakery Story* players bake smarter, not harder. Every visual responds in real time to your slider settings, whether you're chasing fast XP, profit, or just want low-effort bakes.

Clean, interactive, and a little nerdy — just how we like it.

---

## 🧁 Main View

The heart of the report. This is where recipes rise or fall based on what *you* value.

### Layout Map

| Region         | Contents |
|----------------|----------|
| **Top Left**   | Best Recipe card or context message |
| **Top Center** | Appliance dropdown (multi-select) |
| **Top Right**  | Sliders + strategy bookmarks |
| **Middle**     | Column chart: Efficiency Score by Recipe |
| **Right Panel**| Slicers for cook time, profit, XP, etc. |

### Key Visuals

- **Efficiency Bar Chart**  
  - Sorts recipes by real-time score  
  - Hover to see full score breakdown (tooltip below)

- **Best Recipe Card**  
  - Shows the top-ranked option unless filters or weights neutralize it  
  - Automatically updates with every change

- **Sliders (Disconnected Slicers)**  
  - Control weight of each metric (–4 to +4)  
  - Act as **exponents** in the scoring formula  
  - 0 = neutral, negatives = penalize

- **Cook Time Filter**  
  - Limit recipes to a specific range (e.g., 1–4 hours)

- **Appliance Filter**  
  - Pick what appliances you’re using—see only what’s cookable

- **Bookmark Buttons**  
  - Quick toggle between presets:
    - Balanced, Quick Cash, XP Farm, Party Host, Reset  
  - (CTRL+Click required in Power BI)

---

## 🪄 Tooltip (Hover Breakdown)

Hover any bar in the chart to see *why* that recipe scored the way it did.

| Field                | Description |
|---------------------|-------------|
| **Efficiency Score** | Final weighted score |
| **Total / Normalized Profit** | Raw & scaled income |
| **Total / Normalized Cook Time** | Duration in minutes |
| **Total / Normalized Servings** | Plates produced |
| **Total / Normalized XP** | Level-up points |

Think of it as a recipe résumé: here’s the logic behind the rank.

---

## 🔎 Drillthrough (Deep Dive)

Click any recipe to open its profile.

| Insight              | What It Shows                          |
|----------------------|----------------------------------------|
| **Profit per Minute**| Income speed                           |
| **XP per Minute**    | Leveling speed                         |
| **Servings per Minute** | How fast it clears out              |
| **Profit per Serving** | Value per plate                      |
| **XP per Serving**   | XP per customer                        |
| **Total / Normalized Stats** | Raw and scaled metrics         |

**Planned visuals:**
- KPI cards for per-minute / per-serving values  
- Radar chart to visualize trade-offs  
- Fit score: how well this recipe matches your strategy

It’s a sandbox to explore why your pick works—and how it compares across the board.

---

## ✨ Design Touches

- Heart-shaped buttons for bookmarks (because: bakery ❤️)  
- All weights handled via exponents, not just sliders  
- Tooltips and drillthrough make this *feel* like a game  
- Normalized metrics = fair comparisons at any scale  
- One layout, infinite playstyles

---

## 🖼️ Screenshots

| Main View | Tooltip | Drillthrough (Planned) |
|-----------|---------|-------------------------|
| ![Main View](../images/pages/ranked_recipes.png) | ![Tooltip](../images/pages/tooltip_table.png) | *(Coming soon)* |

---

## More Info

Curious about the logic behind the scores?  
Check out [measures_description.md](./measures_description.md) for the full DAX breakdown.

---

This isn’t just a dashboard — it’s a recipe optimizer and strategy engine. All in one scrollable screen.
