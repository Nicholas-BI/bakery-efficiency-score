# 🎨 Visuals Overview

This single-page Power BI report helps *Bakery Story* players bake smarter, not harder. Every visual responds in real time to your slider settings, whether you're chasing fast XP, profit, or just want low-effort bakes.

---

## Main View

The heart of the report. This is where recipes rise or fall based on what *you* value.

### 🗺️ Layout Map (Updated)

| Region          | Contents |
|-----------------|----------|
| **Top Left**    | **Axis Field Selector** — toggles between `Appliance Name` and `Recipe Name` for chart axis |
| **Top Center**  | **Best Recipe** card — shows top result or context-sensitive message |
| **Top Right**   | **Appliance Selector** (multi-select dropdown) and **Cook Time in Minutes** range slicer |
| **Left Panel**  | **Preset Buttons** — heart-shaped bookmarks: Reset, Quick Cash, XP Farm, Party Host, Balanced *(CTRL+Click required)* |
| **Center**      | **Efficiency Score Chart** — bar chart ranking recipes by current weight settings |
| **Right Panel** | **Weight Sliders** — Profit, Cook Time, Servings, XP (used as exponents from –4 to +4) |

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
| **Metric** | Value being weighed |
| **Normalized Value** | [1,2] Range] |
| **Weight Applied** | As an exponent to the normalized value |
| **Placement** | Numerator / Denominator / Ignored |
| **Contribution** | Final value used in the formula |

---

## Design Touches

- Heart-shaped buttons for bookmarks  
- All weights handled via exponents, not just sliders  
- Tooltips and customizability make this *feel* like a game  
- Normalized metrics = fair comparisons at any scale  
- One layout, infinite playstyles

---

## Screenshots

| Main View | Tooltip | Drillthrough (Planned) |
|-----------|---------|-------------------------|
| ![Main View](../images/pages/ranked_recipes.png) | ![Tooltip](../images/pages/tooltip_table.png) | *(Coming soon)* |

---

## More Info

Curious about the logic behind the scores?  
Check out [measures_description.md](./measures_description.md) for the full DAX breakdown.

---

This isn’t just a dashboard — it’s a recipe optimizer and strategy engine. All in one scrollable screen.
