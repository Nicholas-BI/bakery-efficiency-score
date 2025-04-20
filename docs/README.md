# 📚 Documentation Overview

This folder contains all supporting documentation and reference files for the **Bakery Story Efficiency Score** Power BI dashboard. Whether you want to inspect the PBIX, review source data, dive into data modeling, or dissect DAX, everything is here.

---

## 📂 Contents

### 🔧 Files (in `/docs/files`)
- [`bakery_story.pbix`](./files/bakery_story.pbix) — Full Power BI report with all queries, model, DAX, and visuals  
- [`bakery_story_source.xlsx`](./files/bakery_story_source.xlsx) — Raw source data used to build the model  
- [`dax_measures.xlsx`](./files/dax_measures.xlsx) — Export of all DAX measures *(👉 [Download here](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/files/dax_measures.xlsx))*

### 📝 Documentation (in `/docs`)
- [`data_model_overview.md`](./data_model_overview.md) — Fact table, dimension links, and schema design  
- [`power_query.md`](./power_query.md) — ETL design using modular M code and layered queries  
- [`measures_overview.md`](./measures_overview.md) — DAX logic for normalization, weights, and scoring  
- [`visuals_overview.md`](./visuals_overview.md) — Page layouts, sliders, presets, and tooltips  

### 🖼️ Images (in `/docs/images`)
- `bakery_story.png` — Report screenshot  
- `query_dependencies.png` — Power Query dependency diagram  

---

## Getting Started

1. **Open** `bakery_story.pbix` in Power BI Desktop.  
  - 👉 **[Click here to download the Power BI report (.pbix)](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/files/bakery_story.pbix)**  
2. **Review** the data model in the Model view.  
3. **Inspect** Power Query M scripts via [Power Query Overview](./power_query.md).  
4. **Examine** DAX in [Measures Overview](./measures_overview.md)
5. **Explore** report pages with guidance from [Visuals Walkthrough](./visuals_description.md).

---

## Purpose

This documentation is designed to:

- Make it easy to understand how the dashboard is structured.  
- Provide reusable examples of ETL, data modeling, and DAX patterns.  
- Help developers and analysts recreate or extend this solution.

Feel free to clone this folder and adapt any piece to your own Power BI projects.  
