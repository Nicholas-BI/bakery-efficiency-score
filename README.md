# Bakery Story: Recipe Efficiency Dashboard (Power BI)

A Power BI dashboard that ranks *Bakery Story* recipes based on what *you* care about — Profit, Cook Time, Servings, and XP — using dynamic sliders and an exponent-based scoring model built on ratio-normalized metrics.

Whether you're optimizing for fast XP, quick cash, or low-maintenance bakes, this report adapts to your strategy in real time.

---

## How It Works (Under the Hood)

This isn’t just a slicer toy—it’s built on a tailored scoring model using:

- **Ratio-normalized metrics**, shifted +1 to ensure bounded outputs in the [1–2] range  
- **Exponentiation** to apply nonlinear influence based on user-assigned weights  
- **Dynamic DAX logic** that adapts to filters, slicers, and context-aware behavior

The result is a responsive, mathematically robust model that adjusts instantly to reflect your goals.

---

## What Is Bakery Story?

*Bakery Story* is a mobile game where you run a virtual bakery—cooking recipes, serving customers, earning coins, and leveling up. Each recipe is unique: some cook faster, some serve more customers, others yield more profit or XP.

But appliances are limited, cook times vary, and customer arrival is fixed.

So… which recipe is *best*?

---

## Why I Made This

This project started with a debate between me and my partner, Stephanie.

She preferred big-batch recipes—less hassle, fewer check-ins. I wanted faster payouts—shorter bakes meant quicker returns. Neither of us was wrong. We just had different priorities.

> What if a dashboard didn’t tell you what the best recipe is?  
> What if it let you define “best,” and adapted to match?

This dashboard does exactly that.

---

## Try It Yourself

- [Download the Power BI report (.pbix)](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/bakery_story.pbix)  
- [Download the DAX measures (.xlsx)](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/dax_measures.xlsx)  
- [Download the source data (.xlsx)](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/bakery_story_source.xlsx)

Open the `.pbix` file in [Power BI Desktop](https://powerbi.microsoft.com/desktop), adjust the sliders, and see the rankings respond instantly.

---

## What This Dashboard Does

This is a fully dynamic recipe-ranking tool that adapts to your priorities. Whether you're focused on profit, speed, volume, or XP, the scoring model recalculates and ranks recipes based on your input.

Key features include:

- Slider-based control over Profit, Cook Time, Servings, and XP  
- Preset strategies like *Quick Cash*, *XP Farm*, and *Balanced*  
- Appliance-level filtering and cook-time constraints  
- Real-time ranking updates  
- Score breakdown tooltips and measure exports for deeper analysis

---

## Data Model Overview

The report follows a clean star schema for fast, reliable filtering and DAX execution:

**Fact Table**  
- `Fact_Bakery` — Recipe-level metrics and computed values

**Dimension Tables**  
- `Dim_Recipe` — Static recipe attributes  
- `Dim_Appliance` — Appliance types

**Disconnected Weight Tables**  
- `ProfitWeight`, `CookTimeWeight`, `ServingsWeight`, `XPWeight` — Used for slicers

**Helper Tables**  
- `Metrics`, `Axis Field Selector`, `Measure Table` — Support layout and interactivity

See: [Data Model Description](./docs/data_model_description.md)

---

## Scoring Logic

Each recipe receives a dynamic efficiency score based on your weight settings:

1. Normalize each metric
