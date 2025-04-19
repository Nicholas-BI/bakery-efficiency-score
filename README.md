# 🍰 Bakery Story: Recipe Efficiency Report (Power BI)

A Power BI report that ranks *Bakery Story* recipes based on what *you* care about — Profit, Cook Time, Servings, and XP — using dynamic sliders and an exponent-based scoring model built on ratio-normalized metrics.

Whether you're optimizing for fast XP, quick cash, or low-maintenance bakes, this report adapts to your strategy in real time.

---

## What Is Bakery Story?

*Bakery Story* is a mobile game where you run a virtual bakery—cooking recipes, serving customers, earning coins, and leveling up. Each recipe is unique: some cook faster, some serve more customers, others yield more profit or XP.

But appliances are limited, cook times vary, and customer arrival is fixed.

So… which recipe is *best*?

---

## Why I Made This

This project started with a debate between me and my partner, Stephanie.

She preferred big-batch recipes—less hassle, fewer check-ins. I wanted faster payouts—shorter bakes meant quicker returns. Neither of us was wrong. We just had different priorities.

> What if a report didn’t tell you what the best recipe is?  
> What if it let you define “best,” and adapted to match?

This report does exactly that.

---

## What This Report Does

This is a fully dynamic recipe-ranking tool that adapts to your priorities. Whether you're focused on profit, speed, volume, or XP, the scoring model recalculates and ranks recipes based on your input.

**Key features:**
- Slider-based control over Profit, Cook Time, Servings, and XP  
- Preset strategies like *Quick Cash*, *XP Farm*, and *Balanced*  
- Appliance-level filtering and cook-time constraints  
- Real-time ranking updates  
- Score breakdown tooltips and exported DAX measures for transparency

---

## How It Works (Under the Hood)

This isn’t just a slicer toy—it’s built on a tailored scoring model using:

- **Ratio-normalized metrics**, shifted +1 to ensure bounded outputs in the [1–2] range  
- **Exponentiation** to apply nonlinear influence based on user-assigned weights  
- **Dynamic DAX logic** that adapts to filters, slicers, and context-aware behavior

The result is a responsive, mathematically robust model that adjusts instantly to reflect your goals.

---

## Scoring Logic

Each recipe receives a dynamic efficiency score based on your weight settings:

1. Normalize each metric to a [1–2] range  
2. Raise each to its selected exponent (positive = favor; negative = penalize)  
3. Multiply the numerators, divide by the denominators  
4. Rank recipes by final score in current filter context

📄 See: [Measures Overview](./docs/measures_overview.md)  
📥 Download: [dax_measures.xlsx](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/dax_measures.xlsx)

---

## Preset Strategies

| Strategy     | Profit | Cook Time | Servings | XP | Description                          |
|--------------|--------|-----------|----------|----|--------------------------------------|
| Quick Cash   | 10     | –10       | –5       | 3  | Maximize revenue, minimize wait time |
| XP Farm      | 2      | –5        | –5       | 10 | Level up quickly with short bakes    |
| Party Host   | 2      | –5        | 10       | 0  | Maximize servings for events         |
| Balanced     | 5      | –5        | 3        | 3  | A general-purpose optimization        |

---

## Data Model Overview

The report follows a clean star schema for efficient filtering and high-performance DAX:

**Fact Table**  
- `Fact_Bakery` — Recipe-level metrics and computed values

**Dimension Tables**  
- `Dim_Recipe` — Static recipe attributes  
- `Dim_Appliance` — Appliance types

**Disconnected Weight Tables**  
- `ProfitWeight`, `CookTimeWeight`, `ServingsWeight`, `XPWeight` — Used for slicers

**Helper Tables**  
- `Metrics`, `Axis Field Selector`, `Measure Table` — Support layout and interactivity

📄 See: [Data Model Description](./docs/data_model_description.md)

---

## Power Query & ETL

All transformations are handled in Power Query using a modular, transparent approach:

- Source → Base → Output  
- Explicit typing and descriptive step names  
- Designed for reusability and clarity

📄 See: [Power Query Overview](./docs/power_query.md)

---

## Report Design

- One-page interactive layout with slicers and filters  
- Tooltip overlays for full score transparency  
- Bookmark toggles for preset strategies  
- Theming and visuals inspired by the game’s design

📄 See: [Visuals Walkthrough](./docs/visuals_description.md)

---

## 📥 Try It Yourself

- 📥 [Download the Power BI report (.pbix)](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/bakery_story.pbix)  
- 📥 [Download the DAX measures (.xlsx)](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/dax_measures.xlsx)  
- 📥 [Download the source data (.xlsx)](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/bakery_story_source.xlsx)

Open the `.pbix` file in [Power BI Desktop](https://powerbi.microsoft.com/desktop), adjust the sliders, and watch the rankings adapt.

---

## ▶️ Getting Started

1. **Clone the repository**  
   `git clone https://github.com/Nicholas-BI/bakery-efficiency-score.git`  
   *(Or download individual files using the links above)*

2. Open `bakery_story.pbix` in [Power BI Desktop](https://powerbi.microsoft.com/desktop)  
3. Adjust the sliders to reflect your strategy  
4. Explore the rankings, tooltips, and strategy bookmarks

---

## 📁 Repository Contents

All key sections and files in this project:

- [🍰 Introduction](#-bakery-story-recipe-efficiency-report-power-bi)  
- [What Is Bakery Story?](#what-is-bakery-story)  
- [Why I Made This](#why-i-made-this)  
- [What This Report Does](#what-this-report-does)  
- [How It Works (Under the Hood)](#how-it-works-under-the-hood)  
- [Scoring Logic](#scoring-logic)  
- [Preset Strategies](#preset-strategies)  
- [Data Model Overview](#data-model-overview)  
- [Power Query & ETL](#power-query--etl)  
- [Report Design](#report-design)  
- [📥 Try It Yourself](#-try-it-yourself)  
- [▶️ Getting Started](#️-getting-started)  
- [📁 Repository Contents](#-repository-contents)  
- [Screenshots](#screenshots)  
- [Contributing](#contributing)  
- [License](#license)

---

## Screenshots

| Ranked Recipes View                             | Control Panel (Sliders & Bookmarks)           |
|--------------------------------------------------|------------------------------------------------|
| *(Add image here if needed)*                     | *(Add image here if needed)*                  |

---

## Contributing

Have feedback or ideas for improvement?  
Feel free to open an issue or submit a pull request.

---

## License

Licensed under [Creative Commons BY-NC 4.0](./LICENSE)  
Free to use, modify, and share for non-commercial purposes with attribution.
