# 🍰 Bakery Story: Recipe Efficiency Dashboard (Power BI)

A Power BI dashboard that ranks *Bakery Story* recipes based on what *you* care about — Profit, Cook Time, Servings, and XP — using dynamic sliders and an exponent-based scoring model built on ratio-normalized metrics.

Whether you want fast XP, quick cash, or low-maintenance bakes, this report adapts to your strategy—on the fly.

---

## 📱 What Is Bakery Story?

*Bakery Story* is a mobile game where you run a virtual bakery — cooking recipes, serving customers, earning coins, and leveling up. Every recipe is different: some cook faster, some serve more customers, some offer higher profits, and some are great for XP.

But ovens are limited, cook times vary, and customers arrive at a fixed pace.

So… which recipe is *best*?

---

## 🧠 Why I Made This

This project started with a debate between me and my partner, Stephanie.

She liked big-batch recipes — fewer check-ins, less hassle. I saw them as a delay — you don’t get paid until the *last* serving is eaten. I wanted fast payouts; she wanted minimal maintenance.

Neither of us was wrong — we just had different goals.

> What if a dashboard didn’t tell you what the best recipe is?  
> What if it let you define “best,” and adapted to match?

This report does exactly that.

---

## 🔽 Try It Yourself

👉 **[Download the Power BI report (.pbix)](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/bakery_story.pbix)**  
👉 **[Download the DAX measures (.xlsx)](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/dax_measures.xlsx)**  
👉 **[Download the source data (.xlsx)](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/bakery_story_source.xlsx)**

Open the `.pbix` in [Power BI Desktop](https://powerbi.microsoft.com/desktop), tweak the sliders, and see the rankings shift instantly.

---

## 🧁 What This Dashboard Does

It’s a dynamic recipe-ranking tool that adapts to **your priorities**.  
Whether you care most about profits, speed, servings, or XP, the scoring logic adjusts to match.

You can:
- Adjust weights for Profit, Cook Time, Servings, and XP  
- Filter by appliance or cook-time  
- Toggle preset strategies like *Quick Cash* or *XP Farm*  
- See live rankings and full score breakdowns  
- Inspect the math via tooltips or exported DAX

---

## 🧱 Data Model

The report follows a clean star schema for efficient filtering and logic:

- **Fact Table**  
  - `Fact_Bakery` — One row per recipe, with calculated totals

- **Dimension Tables**  
  - `Dim_Recipe` — Name, batch size, and attributes  
  - `Dim_Appliance` — Type of appliance used  

- **Disconnected Weight Tables**  
  - `ProfitWeight`, `CookTimeWeight`, `ServingsWeight`, `XPWeight` — Feed the slicers

- **Helper Tables**  
  - `Metrics`, `Axis Field Selector`, `Measure Table` — Drive interactivity

📄 See: [Data Model Description](./docs/data_model_description.md)

---

## 🧮 Scoring Logic

Each recipe is assigned a score based on your selected preferences:

1. **Normalize** each metric relative to the max (range: 1 to 2)  
2. **Raise** each to the power of its selected weight  
3. **Multiply** numerator metrics; **divide** by denominator metrics  
4. **Rank** based on the final efficiency score  

📄 Full explanation: [Measures Overview](./docs/measures_overview.md)  
📥 Download: [dax_measures.xlsx](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/dax_measures.xlsx)

---

## 🔧 Power Query & ETL

All transformations are handled in Power Query with clear, modular staging:

- Source → Base → Output  
- Explicit typing and clean step naming throughout

📄 See: [Power Query Overview](./docs/power_query.md)

---

## 🎨 Report Design

- Single-page, slicer-driven layout  
- Score breakdown in tooltips  
- Bookmarks for quick strategy swaps  
- Dashboard styling fits the bakery theme  

📄 See: [Visuals Walkthrough](./docs/visuals_description.md)

---

## 🎯 Preset Strategies

| Strategy     | Profit | Cook Time | Servings | XP | Description                          |
|--------------|--------|-----------|----------|----|--------------------------------------|
| Quick Cash   | 10     | –10       | –5       | 3  | Maximize revenue, minimize wait time |
| XP Farm      | 2      | –5        | –5       | 10 | Level up fast with minimal effort    |
| Party Host   | 2      | –5        | 10       | 0  | Max servings for social events       |
| Balanced     | 5      | –5        | 3        | 3  | A general-purpose blend              |

---

## 📁 Repository Contents

Everything lives in the [`/docs`](./docs/) folder:

- [`bakery_story.pbix`](./docs/bakery_story.pbix) — Main Power BI file  
- [`dax_measures.xlsx`](./docs/dax_measures.xlsx) — All DAX logic exported  
- [`bakery_story_source.xlsx`](./docs/bakery_story_source.xlsx) — Source data snapshot  
- [`measures_overview.md`](./docs/measures_overview.md) — Conceptual breakdown of scoring  
- [`data_model_description.md`](./docs/data_model_description.md) — Data structure explained  
- [`power_query.md`](./docs/power_query.md) — ETL flow and query design  
- [`visuals_description.md`](./docs/visuals_description.md) — Page layout and interactions  
- `LICENSE` — Creative Commons BY‑NC 4.0 license  

---

## 🖼️ Screenshots

| Ranked Recipes View                             | Control Panel (Sliders + Bookmarks)           |
|--------------------------------------------------|-----------------------------------------------|
| *(Add image here if needed)*                     | *(Add image here if needed)*                  |

---

## ▶️ Getting Started

1. **Clone the repo**  
   *(or just download the files you want from GitHub or using the links above)*

2. Open `bakery_story.pbix` in [Power BI Desktop](https://powerbi.microsoft.com/desktop)  
3. Use the sliders to reflect your strategy  
4. Explore rankings, tooltips, and bookmarks

📥 [Download Power BI Desktop](https://powerbi.microsoft.com/desktop)

---

## 📄 License

Licensed under [Creative Commons BY‑NC 4.0](./LICENSE).  
Use, adapt, remix freely for **non-commercial** purposes with attribution.

---

## 💡 Contributing

Ideas? Bugs? Open an issue or send a pull request.
