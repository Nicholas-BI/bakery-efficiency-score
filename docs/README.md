# Documentation Overview

This folder contains all supporting documentation and reference files for the **Bakery Story Efficiency Score** Power BI report. It’s designed to be transparent, modular, and easy to explore—whether you're reviewing the data model, DAX logic, visuals, or source files.

---

## Key Files and Downloads

### Core Assets  
- [Download Report (.pbix)](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/data/bakery_story.pbix) *(direct download)*  
- [Download DAX Measures (.xlsx)](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/data/dax_measures.xlsx) *(direct download)*  
- [Download Source Data (.xlsx)](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/data/bakery_story_source.xlsx) *(direct download)*  

---

## Technical Documentation

Explore specific areas of the build:

- [Data Model Overview](./data_model_overview.md) — Schema layout and table structure  
- [Power Query Overview](./power_query_overview.md) — ETL pipeline and modular query design  
- [Measures Overview](./measures_overview.md) — DAX logic, normalization, weights, and scoring  
- [Visuals Overview](./visuals_overview.md) — Report layout, interactivity, tooltips, and strategy presets

---

## Diagram Reference

These diagrams illustrate key elements of the model and ETL flow:

- [`images/data_model.png`](./images/data_model.png) — Star schema and supporting tables  
- [`images/query_dependencies.png`](./images/query_dependencies.png) — Power Query structure  
- [`images/bakery_story.png`](./images/bakery_story.png) — Screenshot of the final report

---

## Getting Started

1. [Download and open the report (.pbix)](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/data/bakery_story.pbix) in Power BI Desktop
2. Explore the **data model** in the Model view  
3. Review **Power Query** steps and logic  
4. Examine **DAX measures** and scoring logic  
5. Interact with the report visuals and slider-based rankings

---

## Purpose

This documentation serves to:

- Provide full transparency into how the report works  
- Offer reusable patterns for Power BI development (ETL, DAX, layout)  
- Support hiring managers, analysts, and developers in quickly assessing the logic and structure

You're welcome to reuse or adapt these ideas in your own Power BI projects.
