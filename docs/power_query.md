# Power Query Overview

This section documents the ETL (Extract, Transform, Load) layer for the **Bakery Story** report. All transformations were authored using Power Query (M) in Power BI Desktop and follow a modular, source‑to‑dimension/fact structure.

---

## Query Layers

Queries are organized into three logical tiers:

### 🔹 Source and Base Queries
- `base_data.txt` – Raw game export containing all Bakery Story events, filtered to the target date range and trimmed to core columns.

---

### 🔹 Fact Tables
- `fact_sales.txt` – Consolidated in‑game sales transactions, revenue, and XP earned, built from `base_data`.  
- `fact_production.txt` – Bake cycle durations, ingredient usage, and oven utilization metrics derived from `base_data`.

---

### 🔹 Dimension Tables
- `dim_recipe.txt` – Distinct recipes with ingredient mappings, category tags, and cooking parameters.  
- `dim_ingredient.txt` – Ingredient metadata including cost, category, and package size.  
- `dim_customer.txt` – Player/customer segmentation attributes and behavior flags.  
- `dim_oven.txt` – Oven/machine characteristics, performance ratings, and upgrade levels.  
- `dim_shop.txt` – Bakery shop metadata such as region, tier, and layout configuration.

---

## Query Dependency Structure

The diagram below illustrates how source queries flow into fact and dimension tables:

![Query Dependency Diagram](../images/power_query/query_dependencies.png)

This clear separation of responsibilities promotes maintainability, performance, and ease of debugging.

---

## Available M Code

Each `.txt` file in this folder contains the full M code used to generate its corresponding table:

- [base_data.txt](./base_data.txt)  
- [fact_sales.txt](./fact_sales.txt)  
- [fact_production.txt](./fact_production.txt)  
- [dim_recipe.txt](./dim_recipe.txt)  
- [dim_ingredient.txt](./dim_ingredient.txt)  
- [dim_customer.txt](./dim_customer.txt)  
- [dim_oven.txt](./dim_oven.txt)  
- [dim_shop.txt](./dim_shop.txt)  

> _Note: Filenames and descriptions above are placeholders—adjust to match your actual query names._

---

## Notes and Conventions

- **Early Typing**: All date/time fields are cast to `datetime` at the source layer to ensure relationship integrity.  
- **Consistent Keys**: Primary keys (e.g., `RecipeID`, `IngredientID`, `OvenID`, `ShopID`) are explicitly cast to prevent schema mismatches.  
- **Descriptive Steps**: Each transformation step uses meaningful names to aid readability and debugging.  
- **Source‑Level Cleanup**: Perform cleansing, filtering, and type conversions as early as possible to keep downstream logic lean.

---

## Related Documentation

- [📄 Data Model Overview](../docs/data_model_description.md) *(placeholder)*  
- [📄 DAX Measures and Logic](../docs/measures_description.md) *(placeholder)*  
- [📄 Visuals Description](../docs/visuals_description.md) *(placeholder)*  
- [📄 SQL Snippets](../docs/sql.txt) *(placeholder)*  
