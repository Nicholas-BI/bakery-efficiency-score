# Bakery Story: Recipe Efficiency Score (Power BI)

A Power BI report that helps you find the best recipes in *Bakery Story* based on what *you* care about. Customize real-time rankings with interactive sliders and a nonlinear scoring model built on ratio-normalized metrics.

---

![Ranked Recipes](./docs/images/bakery_story.png)

---

## What’s the Game?

In *Bakery Story*, you’re running a virtual bakery focused on cooking, serving, leveling up, and trying to make the most of limited appliances.

Each recipe has tradeoffs: cook time, servings, XP, profit. So... what’s the *best* recipe?

This report lets you decide.

---

## Why I Built This

After a spirited debate with my partner (low effort vs. high yield), I built this to settle the score—and make the whole strategy more transparent.

Now you can adjust the weights and *see* how different goals impact the rankings.

---

## What It Tracks

**Dynamic recipe rankings based on your input:**
- Sliders for Profit, Cook Time, Servings, and XP  
- Preset strategies (Quick Cash, XP Farm, etc.)  
- Appliance and cook-time filters  
- Nonlinear exponent-based scoring  
- Full logic exposed in tooltips

---

## Try It

1. Download 🔗 [Power BI Desktop](https://powerbi.microsoft.com/desktop)  
2. Download 📥 [bakery_story.pbix](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/data/bakery_story.pbix) 
3. Tweak sliders and explore strategies  
4. Review tooltips and scoring logic

---

## How It Works

Each recipe’s score is calculated in four steps:

1. Total up raw values  
2. Normalize each metric to the [0–1] range  
3. Apply user-selected exponents (from sliders)
4. Raise values to those weights
5. Multiply weighted metrics, divide by penalized ones  
6. Rank all results in real time

📄 [See Measures Overview](./docs/measures_overview.md)  
📥 [Download DAX Measures (.xlsx)](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/data/dax_measures.xlsx) 

---

## Preset Strategies

Each strategy applies a different weighting profile:

| Strategy     | Profit | Cook Time | Servings | XP | Description                    |
|--------------|--------|-----------|----------|----|--------------------------------|
| Quick Cash   | 20     | –20       | –5       | 1  | Maximize profit, minimize time |
| XP Farm      | 5      | –20       | –5       | 20 | Fast XP with short bakes       |
| Party Host   | 1      |   0       | 20       | 1  | Max servings for events        |
| Balanced     | 2      | –1        | -1       | 2  | Well-rounded optimization      |

---

---

## Layout Features

All visuals are packed into a single, fully interactive report page:

- **Slider Controls** – Adjust weights for Profit, XP, Servings, and Cook Time  
- **Strategy Presets** – One-click bookmarks for common scoring strategies  
- **Ranking Chart** – Recipes re-sort live as weights change  
- **KPI Summary Cards** – Show total cook time and projected earnings  
- **Tooltips** – Transparent, step-by-step breakdowns of each score  
- **Bookmark Reset** – Quickly revert to the default view  

📄 Learn more in the [Visuals Overview](./docs/visuals_overview.md)

---

## Data Model

Simple star schema focused on recipe scoring:

### Fact Table
- `Fact_Bakery` – Recipes, metrics, and results  

### Dimensions
- `Dim_Recipe`, `Dim_Appliance` - Metadata

### Helpers
- `ProfitWeight`, `CookTimeWeight`, etc. – Disconnected slicers  
- `Metrics`, `Axis Selector`, `Measure Table` – Utility support

📄 [See Data Model Overview](./docs/data_model_overview.md)

---

## ETL Pipeline (Power Query)

Modular and reusable:

- Base files: `dim_recipe.txt`, `dim_appliance.txt`, `fact_bakery.txt`  
- Transformations follow Source → Staging → Output pattern  
- Query dependencies visualized below

📄 [See Power Query Overview](./docs/power_query_overview.md)  

---

## Technologies

- Power BI Desktop  
- DAX
- Dax Studio
- Power Query (M)  
- Excel  
- GitHub for documentation  

---

## Repo Contents

- [Download Report (.pbix)](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/data/bakery_story.pbix) *(direct download)*  
- [Download DAX Measures (.xlsx)](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/data/dax_measures.xlsx) *(direct download)*  
- [Download Source Data (.xlsx)](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/data/bakery_story_source.xlsx) *(direct download)*  
- [`docs/images`](./docs/images) – Visuals and diagrams

---

### Explore Other Sections

- [`docs/data_model_overview.md`](./docs/data_model_overview.md) – Table relationships  
- [`docs/measures_overview.md`](./docs/measures_overview.md) – DAX logic  
- [`docs/power_query_overview.md`](./docs/power_query_overview.md) – ETL design  
- [`docs/visuals_overview.md`](./docs/visuals_overview.md) – Layout and interactions  

---

## License & Use

[Creative Commons BY-NC 4.0](./LICENSE)  
For educational/demo purposes. Not for resale or redistribution.
