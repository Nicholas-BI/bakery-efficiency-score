# 📊 Bakery Story: Recipe Efficiency Dashboard (Power BI)

A Power BI dashboard for *Bakery Story* players that ranks recipes based on your personal goals—Profit, Cook Time, Servings, and XP—using dynamic sliders and exponent‑based scoring.



## 📁 Repository Contents

- `README.md` – Project overview and screenshots  
- [`/docs`](./docs/) – Supporting documentation  
  - [Data Model Description](./docs/data_model_description.md)  
  - [Measures Overview](./docs/measures_description.md)  
  - [Visuals Walkthrough](./docs/visuals_description.md)  
  - [SQL Snippets](./docs/sql.txt) *(placeholder)*  
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

## 📝 Project Overview

A dynamic recipe‑ranking tool that lets **you** decide which metrics matter, then instantly updates recommended bakes.  
Optimize for fast revenue, XP farming, large events, or a balanced approach—directly in Power BI.

---

## 🚀 Key Features

- **📊 Dynamic Ranking** – Real‑time reorder based on slider weights  
- **🎛️ Slider Controls** – Adjust Profit, Cook Time, Servings, and XP  
- **⚖️ Exponent‑Based Scoring** – Non‑linear weighting for greater impact  
- **🔎 Advanced Filtering** – By appliance (oven, fryer, drink machine) and cook‑time window  
- **🔘 Preset Strategies** – Quick Cash, XP Farm, Party Host, Balanced  
- **📈 Interactive Tooltips** – Display full score breakdown  
- **🔢 Fair Normalization** – Consistent ratios across all units

---

## 📊 Data Model Overview

A clean star schema for performant analysis:

- **Fact Tables**  
  - `fact_sales` – Revenue & XP transactions per bake  
  - `fact_production` – Cook time & appliance usage  

- **Dimension Tables**  
  - `dim_recipe`, `dim_ingredient`, `dim_customer`, `dim_oven`, `dim_shop`  

- **Supporting Tables**  
  - Calendar, presets, disconnected slicers  

> See [Data Model Description](./docs/data_model_description.md)

---

## 🔍 Scoring Logic (DAX Strategy)

1. **Normalize** each metric as a ratio  
2. **Raise** to the power of its slider weight  
3. **Combine** – multiply positives, divide negatives  
4. **Rank** by resulting score  

> Full formulas in [Measures Overview](./docs/measures_description.md)  
> Browse measure list: [dax_measures.xlsx](./docs/dax_measures.xlsx)

---

## 🔄 ETL & Power Query

Modular Power Query (M) workflows transform source data into facts & dimensions:

- **Layers:** Source → Base → Fact → Dimension  
- **Conventions:** Early type casting, descriptive steps, key normalization  

> ETL details: [Power Query Overview](./power_query/README.md)  
> Dependency graph:  
> ![Query Dependencies](./images/power_query/query_dependencies.png)

---

## 🖼️ Visuals Walkthrough

In-depth look at page layouts, slicers, and bookmarks:

> See [Visuals Walkthrough](./docs/visuals_description.md)

---

## 🎯 Preset Strategies

| Strategy     | Profit | Cook Time | Servings | XP | Description                       |
|--------------|--------|-----------|----------|----|-----------------------------------|
| Quick Cash   | 4      | –4        | –2       | 1  | Maximize revenue, minimize waits  |
| XP Farm      | 1      | –2        | –2       | 4  | Fast leveling, avoid long bakes   |
| Party Host   | 1      | –2        | 4        | 0  | Serve large crowds                |
| Balanced     | 2      | –2        | 1        | 1  | Even trade‑off across metrics     |

---

## 📷 Screenshots

| Main View                                          | Slider & Preset Panel                          |
|----------------------------------------------------|-------------------------------------------------|
| ![Ranked Recipes](./images/pages/ranked_recipes.png)  | ![Controls](./images/pages/sliders_and_bookmarks.png) |

---

## 🚀 Getting Started

1. **Clone** this repository  
2. **Open** `BakeryStory_Efficiency.pbix` in Power BI Desktop  
3. **Adjust** sliders to your preferred weights  
4. **Explore** ranked recipes and hover for details  

> Download Power BI Desktop: https://powerbi.microsoft.com/desktop/

---

## 🔐 License

Licensed under [CC BY‑NC 4.0](./LICENSE).  
Use, adapt, and share for non‑commercial purposes with attribution.

---

## 📣 Contributing

Feedback, custom presets, or collaboration inquiries?  
Open an issue or submit a pull request!
