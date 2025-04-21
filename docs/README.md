# 📚 Documentation Overview

This folder contains all supporting docs and reference files for the **Bakery Story Efficiency Score** Power BI report. Whether you’re exploring the model, reviewing DAX, or grabbing the PBIX—everything you need is right here.

---

## Contents

### `/docs/data`
- [`bakery_story.pbix`](../data/bakery_story.pbix) — Full Power BI report with queries, model, DAX, and visuals  
- [`bakery_story_source.xlsx`](../data/bakery_story_source.xlsx) — Raw recipe data used for modeling  
- [`dax_measures.xlsx`](../data/dax_measures.xlsx) — Export of all DAX measures  

### Documentation
- [`data_model_overview.md`](./data_model_overview.md) — Schema layout, fact/dim tables, and logic  
- [`power_query_overview.md`](./power_query_overview.md) — ETL design and modular M queries  
- [`measures_overview.md`](./measures_overview.md) — DAX breakdown: normalization, weights, scoring  
- [`visuals_overview.md`](./visuals_overview.md) — Report layout, sliders, tooltips, and strategies

### Images
- `/images/bakery_story.png` — Report screenshot  
- `/images/query_dependencies.png` — Power Query structure diagram

---

## Getting Started

1. **Download and open** [`bakery_story.pbix`](../data/bakery_story.pbix) in Power BI Desktop  
2. **Explore** the data model using the Model view  
3. **Review** queries in [Power Query Overview](./power_query_overview.md)  
4. **Inspect** scoring logic in [Measures Overview](./measures_overview.md)  
5. **Navigate** visuals with [Visuals Overview](./visuals_overview.md)

---

## Purpose

This documentation is here to:
- Explain how the report works—clearly and completely  
- Offer reusable ETL, modeling, and DAX patterns  
- Help analysts recreate or extend this build

Feel free to reuse or adapt anything in here for your own Power BI projects.
