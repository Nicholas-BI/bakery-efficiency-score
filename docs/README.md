# Documentation Overview

This folder contains all supporting documentation and reference files for the **Bakery Story Efficiency Score** Power BI dashboard. Whether you want to inspect the PBIX, review source data, dive into data modeling, or dissect DAX, everything is here.

---

## Contents

- [`bakery_story.pbix`](./bakery_story.pbix)  
  The main Power BI Desktop file with all queries, data model, DAX measures, and visuals.

- [`bakery_story_source.xlsx`](./bakery_story_source.xlsx)  
  Raw source export of Bakery Story data used to build the model.

- [Data Model Description](./data_model_description.md)  
  Overview of the single fact table (`Fact_Bakery`), parameter tables, relationships, and key fields.

- [Power Query Overview](./power_query.md)  
  Explanation of the modular M code: source, base, fact, and dimension queries, plus dependency diagrams.

- [Measures Overview](./measures_overview.md)  
  Breakdown of core DAX: normalization, exponent weighting, dynamic numerator/denominator logic, and final score.

- [DAX Measures File](./dax_measures.xlsx)
- 👉 **[Click here to download the DAX measures (.xlsx)](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/dax_measures.xlsx)**  
  Full export of all DAX measures—from base metrics to display helpers.

- [Visuals Walkthrough](./visuals_description.md)  
  A guided tour of the report pages: slider controls, presets, tooltips, and interaction patterns.

---

## Getting Started

1. **Open** `bakery_story.pbix` in Power BI Desktop.  
2. **Review** the data model in the Model view.  
3. **Inspect** Power Query M scripts via [Power Query Overview](./power_query.md).  
4. **Examine** DAX in [Measures Overview](./measures_description.md) or the exported `[dax_measures.xlsx](./dax_measures.xlsx)`.  
5. **Explore** report pages with guidance from [Visuals Walkthrough](./visuals_description.md).

---

## Purpose

This documentation is designed to:

- Make it easy to understand how the dashboard is structured.  
- Provide reusable examples of ETL, data modeling, and DAX patterns.  
- Help developers and analysts recreate or extend this solution.

Feel free to clone this folder and adapt any piece to your own Power BI projects.  
