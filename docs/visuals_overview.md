# Visuals Overview

This single-page Power BI report ranks recipes in real time based on your priorities—XP, profit, servings, or low-maintenance bakes. Every visual responds instantly to your slider settings, filters, and presets.

---

## Report Layout

| Region           | Contents                                                                 |
|------------------|--------------------------------------------------------------------------|
| **Top Row**       | Key Metrics – Servings/XP/Profit per Minute & per Coin, Minutes per Coin |
| **Upper Left**    | Recipe Selector – searchable list of available recipes                   |
| **Upper Center**  | Best Recipe Card and Appliance Selector – shows best recipe, selection, and filters    |
| **Middle Left**   | Axis Field Selector – toggle between Appliance or Recipe                 |
| **Lower Left**    | Preset Buttons – strategy bookmarks: Reset, Quick Cash, XP Farm, etc.    |
| **Center**        | Score by Recipe or Appliance Chart – visual ranking based on user-weighted efficiency |
| **Right Panel**   | Weight Sliders – Profit, Cook Time, Servings, XP                         |


---

## Key Visuals

### Efficiency Chart
- Ranks recipes by real-time score  
- Hover to reveal score breakdown  
- Fully filter-aware and responsive

### Best Recipe Card
- Always shows the top result  
- Handles ties, filters, or neutral weights with clear feedback  
- Updates instantly with every change

### Weight Sliders
- Adjust weights (–20 to +20) for each trait  
- Values act as **exponents** in the scoring formula  
- 0 = neutral, negatives penalize

### Cook Time & Appliance Filters
- Limit recipes to time ranges (e.g., 30–120 minutes)  
- Show only recipes for appliances you’ve unlocked

### Preset Buttons
- Switch strategies on the fly:
  - **Quick Cash**  
  - **XP Farm**  
  - **Party Host**  
  - **Balanced**  
  - **Reset**

---

## Tooltip Breakdown

Hover any bar to see exactly how a score was built.

| Field         | Description                              |
|---------------|------------------------------------------|
| **Metric**    | The trait being scored                   |
| **Normalized**| Scaled to [1–2] range                    |
| **Weight**    | Your selected exponent                   |
| **Placement** | Role in formula: numerator, denominator, or ignored |
| **Value**     | Final contribution to the overall score  |

---

## Design Details

- All sliders are disconnected slicers used as exponents  
- Tooltips explain every score, step by step  
- Bookmarks use themed icons (hearts)  
- Normalization enables fair comparisons across all values  
- One page, infinite strategies

---

## Screenshot

![Bakery Story Screenshot](./images/bakery_story.png)

---

### Explore Other Sections

- 📄 [`See Data Model Overview`](./docs/data_model_overview.md) – Table relationships  
- 📄 [`See Measures Overview`](./docs/measures_overview.md) – DAX logic  
- 📄 [`See Power Query Overview`](./docs/power_query_overview.md) – ETL design  

---
