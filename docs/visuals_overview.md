# Visuals Overview

This single-page Power BI report ranks recipes in real time based on your priorities—XP, profit, servings, or low-maintenance bakes. Every visual responds instantly to your slider settings, filters, and presets.

---

## Report Layout

| Region         | Contents                                                                 |
|----------------|--------------------------------------------------------------------------|
| **Top Left**   | Axis Selector – toggle between Appliance or Recipe                       |
| **Top Center** | Best Recipe Card – shows top result or fallback message                  |
| **Top Right**  | Appliance Selector and Cook Time slicer                                  |
| **Left Panel** | Preset Buttons – strategy bookmarks: Quick Cash, XP Farm, etc.           |
| **Center**     | Efficiency Chart – recipe rankings based on your weights                 |
| **Right Panel**| Weight Sliders – Profit, Cook Time, Servings, XP                         |

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

## More Info

Want the full logic?

📄 [See Measures Overview](./measures_overview.md)

This isn’t just a dashboard—it’s a strategy engine built for play.

---

### Explore Other Sections

- [`docs/data_model_overview.md`](./docs/data_model_overview.md) – Table relationships  
- [`docs/measures_overview.md`](./docs/measures_overview.md) – DAX logic  
- [`docs/power_query_overview.md`](./docs/power_query_overview.md) – ETL design  
- [`docs/visuals_overview.md`](./docs/visuals_overview.md) – Layout and interactions

---
