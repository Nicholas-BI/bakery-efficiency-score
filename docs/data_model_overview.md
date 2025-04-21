# 🧱 Data Model Overview

This report uses a lean star schema—just one fact table, a few dimensions, and disconnected weight slicers—but it’s packed with interactive logic behind the scenes.

Curious how the scoring works or how sliders plug into DAX? You’re in the right spot.

[Click here to download the source data](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/files/bakery_story.pbix)  

---

## Fact Table

### `Fact_Bakery`
- One row per recipe  
- Core attributes:
  - `Income`, `Cost` → used to compute Profit  
  - `Cook Time` (in minutes)  
  - `Servings` per batch  
  - `XP` gained  
  - Recipe name and Appliance type  
- Drives all scoring and visual logic  

---

## Dimensions

### `Dim_Recipe`
- One row per recipe name  
- Supports slicers, titles, and filtering  

### `Dim_Appliance`
- Maps recipes to their appliance (e.g. oven, stove)  
- Used to filter by equipment availability  

---

## Weight Tables (What-If Sliders)

Created using `GENERATESERIES`, each weight table powers a disconnected slider for:

- `ProfitWeight`  
- `CookTimeWeight`  
- `ServingsWeight`  
- `XPWeight`  

**Weights range from –20 to 20**, controlling how much each metric influences the score:

- Positive → Favor (goes in numerator)  
- Negative → Penalize (goes in denominator)  
- Zero → Ignore the metric entirely  

Used with `SELECTEDVALUE()` to inject logic directly into DAX without affecting relationships.

### Example: `ProfitWeight`
```DAX
ProfitWeight = GENERATESERIES(-20, 20, 1)
