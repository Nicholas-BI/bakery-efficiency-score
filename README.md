# Power BI: Bakery Story Efficiency Score

This Power BI project models product efficiency in the mobile game *Bakery Story*. Users can rank recipes based on customizable criteria such as profit, cooking time, servings, and experience (XP) gained. Weight sliders let players express their playstyle priorities—whether chasing fast cash, XP, or passive income—and dynamically re-rank recipes in real time.

---

## Note

This dashboard is shared for portfolio purposes only. It is not affiliated with Storm8 or intended for commercial use.

---

## Repository Contents

- `README.md` – Project overview and screenshots  
- [`/docs`](./docs/) – Supporting documentation for model, DAX, and visuals  
  - [Data Model Description](./docs/data_model_description.md)  
  - [Measures Overview](./docs/measures_description.md)  
  - [Visuals Walkthrough](./docs/visuals_description.md)  
- [`/power_query`](./power_query/) – Power Query M code and ETL logic  
- [`/images`](./images/) – Report screenshots and diagrams  
- [DAX Measures File](./docs/dax_measures.xlsx) – Full export of all measures

---

## Project Overview

This report helps *Bakery Story* players optimize their gameplay by comparing recipe efficiency under different playstyle preferences. Users assign weights to key metrics—Profit, Cook Time, Servings, XP—and instantly see a ranked list of recipes based on their priorities. All calculations are normalized and dynamic.

---

## Key Features

- Fully dynamic weighting system via slicers  
- Bookmark presets for different playstyles (e.g. Quick Cash, XP Farm)  
- Real-time recipe ranking by user preferences  
- Interactive tooltips and supporting visuals  
- Exponent-based scaling for greater differentiation  
- Ratio-based normalization to preserve relative performance

---

## Data Model Overview

The model is based on a single fact table with supporting What-If parameter tables:

- **Fact Tables:**  
  - `Fact_Bakery` – One row per recipe with attributes for profit, XP, servings, and time  

- **Weight Tables:**  
  - `ProfitWeight`, `CookTimeWeight`, `ServingsWeight`, `XPWeight` – Disconnected What-If tables for user-selected weights  

- **Utility Tables:**  
  - `TimePeriods` (for filtering scenarios or presets)  
  - `Calendar` (basic date table, if time logic is used)  

> See [📄 Data Model Description](./docs/data_model_description.md)

---

## Report Pages

The report includes a single interactive dashboard with weight sliders, bookmark buttons, and a ranked bar chart of recipes.

- **Main Page**  
  - Weight sliders for Profit, Cook Time, Servings, XP  
  - Preset buttons for common playstyles  
  - Recipe table and bar chart ranked by dynamic Efficiency Score  
  - Tooltips showing breakdowns and normalized scores  

> See [📄 Visuals Walkthrough](./docs/visuals_description.md)

---

## DAX Strategy

This report uses a **modular DAX architecture** built around user-adjustable logic. Instead of hardcoded priorities, the ranking logic is driven by relative importance via exponent-weighted scores.

### Measure Structure:

- **Base Measures**  
  - `Total Profit`, `Total XP`, `Total Cook Minutes`, `Total Servings`

- **Normalized Measures**  
  - Ratio-based calculations (e.g., `Normalized Profit = Profit / Max Profit`)  

- **Exponent Scaled**  
  - Each normalized value is raised to the user-defined weight power  
  - Positive weights emphasize high values  
  - Negative weights penalize high values (flip to denominator)

- **Efficiency Score**  
  - Score = (Product of all positively-weighted terms) ÷ (Product of negatively-weighted terms)  

> See [📄 Measures Overview](./docs/measures_description.md)  
> Browse the full list in [📊 dax_measures.xlsx](./docs/dax_measures.xlsx)

---

## Power Query & ETL

Recipe data is derived from in-game values (profit, XP, servings, time), entered manually for modeling purposes. Power Query is used for basic cleanup, typing, and shaping into a single fact table.

> See [📄 ETL Overview](./power_query/README.md)  
> [📷 Query Dependencies](./images/power_query/query_dependencies.png)

---

## Data Privacy

All recipe data is sourced from publicly available in-game information. No sensitive or proprietary data is included.

---

## Technologies Used

- Power BI Desktop  
- DAX (Data Analysis Expressions)  
- Power Query (M)  
- Excel (for initial entry)  
- GitHub for documentation  

---

## Report Screenshots

| Recipe Ranking | Weight Sliders |
|----------------|----------------|
| ![Recipe Ranking](./images/pages/ranked_recipes.png) | ![Sliders](./images/pages/sliders_and_bookmarks.png) |

| Bookmark Presets | Tooltip Breakdown |
|------------------|-------------------|
| ![Presets](./images/pages/bookmarks.png) | ![Tooltip](./images/pages/tooltip.png) |

---

## Purpose

This report is part of a personal portfolio to demonstrate:

- A fully interactive, player-guided efficiency model  
- Use of What-If slicers to parameterize logic  
- Ratio-based normalization and exponent scaling  
- Dynamic DAX for non-business use cases  
- Clear, communicative reporting for a casual audience

