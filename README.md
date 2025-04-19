# Bakery Story: Recipe Efficiency Dashboard (Power BI)

A Power BI dashboard for *Bakery Story* players that ranks recipes based on your personal goals—Profit, Cook Time, Servings, and XP—using dynamic sliders and exponent‑based scoring of ratio-normalized metrics.

---

## Why I Made This

This project started with a conversation between me and my partner, Stephanie.

She liked recipes with huge batch sizes — fewer check-ins, less hassle. I saw them as a delay — you don’t get paid until the *last* serving is eaten, and customers enter at a fixed pace. I wanted fast cash, she wanted low maintenance.

The realization was: neither of us was wrong — we just had different values.

That’s when the idea clicked:

> What if a report didn’t tell you what the best recipe is?  
> What if it let **you decide what “best” means**—and shaped itself around that?

This dashboard does exactly that.

---

## Repository Contents

- `README.md` – Project overview and screenshots  
- [`/docs`](./docs/) – Supporting documentation  
  - [Data Model Description](./docs/data_model_description.md)  
  - [Measures Overview](./docs/measures_description.md)  
  - [Visuals Walkthrough](./docs/visuals_description.md)  
- [`/power_query`](./power_query/) – M code, query structure, and ETL logic  
  - [Power Query Overview](./power_query/README.md)  
  - [Query Dependencies Diagram](./images/power_query/query_dependencies.png)  
- [`/images`](./images/) – Report screenshots and diagrams  
  - `/images/pages/` – Dashboard screenshots  
  - `/images/power_query/` – ETL dependency charts  
- `BakeryStory_Efficiency.pbix` – Power BI Desktop file *(placeholder name)*  
- [DAX Measures File](./docs/dax_measures.xlsx) – Full export of all DAX measures  
- `LICENSE` – Creative Commons BY‑NC 4.0

---

## Project Overview

A dynamic recipe‑ranking tool that lets **you** decide which metrics matter, then instantly updates recommended bakes.  
Optimize for fast revenue, XP farming, large events, or a balanced approach—directly in Power BI.

---

## Key Features

- Dynamic ranking that updates in real-time based on slider weights  
- Slider controls for Profit, Cook Time, Servings, and XP  
- Exponent‑based scoring for non‑linear influence  
- Filter by appliance or cook-time window  
- Preset strategy bookmarks (Quick Cash, XP Farm, Party Host, Balanced)  
- Interactive tooltips with full score breakdown  
- Ratio-based normalization for fair metric scaling

---

## Data Model Overview

This report uses a clean star schema tailored for responsive filtering and flexible metric calculation:

- **Fact Table:**  
  - `Fact_Bakery` – One row per recipe instance, with calculated metrics

- **Dimension Tables:**  
  - `Dim_Recipe` – Recipe attributes (e.g., name, base values)  
  - `Dim_Appliance` – Type of cooking device used  

- **Weight Tables (Disconnected):**  
  - `ProfitWeight`, `CookTimeWeight`, `ServingsWeight`, `XPWeight` — Each stores a list of weight values for slicers

- **Slicer & UI Support Tables:**  
  - `Axis Field Selector`, `Metrics`, `Measure Table` — Help drive layout and interactivity

> See [Data Model Description](./docs/data_model_description.md)

![Data Model Diagram](./images/data_model/bakery_data_model.png)

---

## Scoring Logic (DAX Strategy)

1. Normalize each metric relative to max values  
2. Raise each to the power of its selected weight  
3. Multiply numerator values, divide by denominator values  
4. Rank based on the resulting efficiency score  

> See [Measures Overview](./docs/measures_description.md)  
> Browse the measure list: [dax_measures.xlsx](./docs/dax_measures.xlsx)

---

## ETL & Power Query

The Power Query layer organizes transformations by stage and purpose:

- Source → Base → Fact/Dimension  
- Clean step naming, explicit types, modular logic

> ETL Overview: [Power Query Overview](./power_query/README.md)  
> Dependencies diagram:  
> ![Query Dependencies](./images/power_query/query_dependencies.png)

---

## Visuals Walkthrough

Detailed notes on report layout, slicer design, bookmarks, and the drillthrough + tooltip experience.

> See [Visuals Walkthrough](./docs/visuals_description.md)

---

## Preset Strategies

| Strategy     | Profit | Cook Time | Servings | XP | Description                       |
|--------------|--------|-----------|----------|----|-----------------------------------|
| Quick Cash   | 10     | –10       | –5       | 3  | Maximize revenue, minimize waits  |
| XP Farm      | 2      | –5        | –5       | 10 | Fast leveling, avoid long bakes   |
| Party Host   | 2      | –5        | 10       | 0  | Serve large crowds                |
| Balanced     | 5      | –5        | 3        | 3  | Even trade‑off across metrics     |

---

## Screenshots

| Main View                                          | Slider & Preset Panel                          |
|----------------------------------------------------|-------------------------------------------------|
| ![Ranked Recipes](./images/pages/ranked_recipes.png)  | ![Controls](./images/pages/sliders_and_bookmarks.png) |

---

## Getting Started

1. Clone this repository  
2. Open `BakeryStory_Efficiency.pbix` in Power BI Desktop  
3. Adjust sliders to reflect your priorities  
4. Explore and hover to inspect top-ranked recipes  

> Power BI Desktop: https://powerbi.microsoft.com/desktop/

---

## License

Licensed under [CC BY‑NC 4.0](./LICENSE).  
Free to use, adapt, and share for non‑commercial purposes with attribution.

---

## Contributing

Got feedback, ideas, or tweaks?  
Open an issue or submit a pull request.
