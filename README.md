# 🍰 Bakery Story: Recipe Efficiency Dashboard (Power BI)

A Power BI dashboard that ranks *Bakery Story* recipes based on what *you* care about — Profit, Cook Time, Servings, and XP — using dynamic sliders and an exponent‑based scoring model built on ratio-normalized metrics.

---

## What Is Bakery Story?

*Bakery Story* is a casual mobile game where players run a virtual bakery — cooking recipes, serving customers, earning coins, and leveling up. Every recipe is different: some earn more profit, some cook faster, some serve more customers, and some give better XP.

But here's the catch: you can't cook them all.

So… which recipe is *best*?

---

## Why I Made This

This project started with a conversation between me and my partner, Stephanie.

She liked big-batch recipes — fewer check-ins, less hassle. I saw them as a delay — you don’t get paid until the *last* serving is eaten, and customers arrive at a fixed pace. I wanted fast cash; she wanted low maintenance.

The realization was: neither of us was wrong — we just had different goals.

That’s when the idea clicked:

> What if a report didn’t tell you what the best recipe is?  
> What if it let you define “best” — and adapted to match?

This dashboard does exactly that.

---

## 🔽 Try It Yourself

👉 **[Click here to download the Power BI report (.pbix)](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/bakery_story.pbix)**  
👉 **[Click here to download the DAX measures (.xlsx)](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/dax_measures.xlsx)**  
👉 **[Click here to download the source data (.xlsx)](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/bakery_story_source.xlsx)**

Open the `.pbix` file in [Power BI Desktop](https://powerbi.microsoft.com/desktop), adjust the sliders, and watch the rankings adapt in real time.

---

## 📁 Repository Contents

All files are stored in the [`/docs`](./docs/) folder:

- [`bakery_story.pbix`](./docs/bakery_story.pbix) — Full Power BI report  
- [`dax_measures.xlsx`](./docs/dax_measures.xlsx) — Exported measures for reference  
- [`bakery_story_source.xlsx`](./docs/bakery_story_source.xlsx) — Source data  
- [`measures_overview.md`](./docs/measures_overview.md) — Scoring logic and DAX strategy explained  
- [`data_model_description.md`](./docs/data_model_description.md) — Schema and table roles  
- [`power_query.md`](./docs/power_query.md) — ETL design and transformation notes  
- [`visuals_description.md`](./docs/visuals_description.md) — Report page and visual design  

Also includes:
- `LICENSE` — Creative Commons BY‑NC 4.0 license  
- This `README.md` — Project overview

---

## 🧠 Project Overview

This is a dynamic recipe‑ranking tool that lets **you** decide which metrics matter, then instantly updates recommendations.  
Optimize for fast revenue, XP farming, minimal babysitting, or a balanced approach — directly in Power BI.

---

## 🔧 Key Features

- Slider-based weight control for Profit, Cook Time, Servings, and XP  
- Real-time recipe ranking based on user-defined priorities  
- Exponent‑based scoring for non-linear influence  
- Ratio-normalized metrics for fair comparisons  
- Appliance filtering and preset strategy bookmarks  
- Interactive tooltips with score breakdown

---

## 📊 Data Model

The report uses a clean star schema for optimized filtering and DAX performance:

### Fact Table  
- `Fact_Bakery` — Each row represents a recipe, including totals and derived metrics

### Dimensions  
- `Dim_Recipe` — Recipe name, type, and attributes  
- `Dim_Appliance` — Ovens, mixers, etc.

### Weight Tables (Disconnected)  
- `ProfitWeight`, `CookTimeWeight`, `ServingsWeight`, `XPWeight` — Populate the slicers

### UI Support  
- `Metrics`, `Axis Field Selector`, `Measure Table` — Used for interactivity and toggling views

📄 **Read more:** [Data Model Description](./docs/data_model_description.md)

---

## 🧮 Scoring Logic

1. Sum up each recipe’s profit, cook time, servings, and XP  
2. Normalize each metric between 1 and 2 (relative to context)  
3. Raise each normalized metric to the power of its selected weight  
4. Multiply all “positive” metrics and divide by all “negative” ones  
5. Return the best recipe by efficiency score in current context  

📄 **Details & DAX included in:** [Measures Overview](./docs/measures_overview.md)  
📥 **Download all measures as Excel:** [dax_measures.xlsx](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/dax_measures.xlsx)

---

## 🧼 Power Query / ETL Logic

All transformations are done in Power Query using modular steps:  
- `Source` → `Base Tables` → `Fact & Dimension Output`  
- Each query has a clear role and naming convention  
- All types explicitly defined; no implicit conversions

📄 **Detailed walkthrough:** [Power Query Overview](./docs/power_query.md)

---

## 🎨 Visual Design

- One-page interactive report  
- Bookmark buttons to toggle strategy views  
- Tooltip showing score composition and logic  
- Clean visual layout with bakery theme

📄 **Design notes:** [Visuals Walkthrough](./docs/visuals_description.md)

---

## 🎯 Preset Strategies

| Strategy     | Profit | Cook Time | Servings | XP | Description                       |
|--------------|--------|-----------|----------|----|-----------------------------------|
| Quick Cash   | 10     | –10       | –5       | 3  | Maximize revenue, minimize waits  |
| XP Farm      | 2      | –5        | –5       | 10 | Fast leveling, avoid long bakes   |
| Party Host   | 2      | –5        | 10       | 0  | Serve large crowds                |
| Balanced     | 5      | –5        | 3        | 3  | Even trade‑off across metrics     |

---

## 🖼️ Screenshots

| Ranked Recipes View                             | Control Panel (Sliders + Bookmarks)           |
|--------------------------------------------------|-----------------------------------------------|
| *(add image if desired)*                         | *(add image if desired)*                      |

---

## ▶️ Getting Started

1. Clone this repository  
2. Open `bakery_story.pbix` in Power BI Desktop  
3. Use the sliders to assign weights  
4. Explore rankings and hover for full explanations

📥 [Download Power BI Desktop](https://powerbi.microsoft.com/desktop)

---

## 📄 License

Licensed under [Creative Commons BY‑NC 4.0](./LICENSE).  
Free to use, adapt, and remix for **non-commercial purposes** with attribution.

---

## 💡 Contributing

Have suggestions or ideas?  
Feel free to open an issue or submit a pull request.
