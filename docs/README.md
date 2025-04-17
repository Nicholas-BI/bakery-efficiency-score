# Documentation Overview

This folder contains all supporting documentation for the **Bakery Story Efficiency Score** Power BI dashboard. If you're curious about how the recipe rankings work, what DAX magic is running under the hood, or how the report visuals are structured — this is the place to dig in.

---

## Contents

- [Data Model Description](./data_model_description.md)  
  Overview of the single fact table (`Fact_Bakery`) and its supporting What-If parameter tables for weighting logic. Includes notes on key fields like income, cost, servings, cook time, and XP.

- [Measures Overview](./measures_description.md)  
  Breakdown of the core DAX logic, including normalization, exponent scaling, dynamic numerator/denominator flipping, and the final efficiency score calculation.

- [Visuals Walkthrough](./visuals_description.md)  
  A guided tour through the layout, sliders, bookmark presets, tooltips, and how each visual contributes to gameplay decision-making.

- [DAX Measures File](./dax_measures.xlsx)  
  Full export of all DAX measures used in the model — from base metrics to scoring logic and display helpers.

---

## Purpose

This folder exists to help you understand how the report works behind the scenes. Whether you’re reviewing this for fun, trying to recreate something similar, or just want to geek out about DAX tricks, everything is laid out here for clarity and reuse.

If you're just getting started, we recommend jumping into:

- [Visuals Walkthrough](./visuals_description.md) to get a feel for how players interact with the report  
- [Measures Overview](./measures_description.md) to see how scoring is actually calculated  
