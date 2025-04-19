# Data Model Description

This report uses a lightweight star schema designed to rank recipes based on flexible user input. The model is intentionally simple — just one fact table and a handful of helper tables — but it packs a surprising amount of logic behind the scenes.

If you’re curious about how the score gets calculated or how the sliders connect to DAX, this is the place to look.

---

## Fact Table

### `Fact_Bakery`
- One row per recipe  
- Contains raw attributes:  
  - `Income` and `Cost` → used to calculate profit  
  - `Cook Time` in minutes  
  - `Servings` per dish  
  - `XP` gained when cooking is complete  
- Also includes fields for appliance type and recipe name  
- Used as the core of all scoring logic  

---

## Dimension Tables

### `Dim_Recipe`
- Contains one unique row per recipe name  
- Used for slicers, labels, and dynamic titles  

### `Dim_Appliance`
- Maps each recipe to its appliance (oven, stove, drink machine, etc.)  
- Enables filtering by what equipment you have unlocked  

---

## Weight Tables (What-If Parameters)

Each slider in the report is backed by a What-If Parameter table created using `GENERATESERIES`, allowing users to assign weights to Profit, Cook Time, Servings, and XP on a scale from –20 to 20 in steps of 1.

These weights influence how each metric contributes to the overall efficiency score:
- **Positive weights** favor a metric (push it into the numerator)
- **Negative weights** penalize a metric (push it into the denominator)
- **Zero** effectively disables that metric's influence

This setup gives players complete control over what “best” means to them.

---

### Example — `ProfitWeight`

```DAX
ProfitWeight = GENERATESERIES(-20, 20, 1)
```

This structure:
- Ensures clean, whole-number increments
- Guarantees true zero (no floating-point noise)
- Keeps the slider behavior intuitive and responsive

The same pattern is used for:
- `CookTimeWeight`
- `ServingsWeight`
- `XPWeight`

Each table is disconnected from the data model and accessed via `SELECTEDVALUE()` in DAX to feed directly into the scoring formula.

## Measure Table

### `Measure Table`
- Dummy table used to hold display measures (like the current “best recipe” text)  
- Doesn’t connect to anything — just keeps things tidy

---

## Relationship Summary

| From                      | To                             | Type         | Direction |
|---------------------------|----------------------------------|--------------|-----------|
| `Fact_Bakery[Recipe]`     | `Dim_Recipe[Recipe Name]`       | Many-to-One  | Single     |
| `Fact_Bakery[Appliance]`  | `Dim_Appliance[ApplianceName]`  | Many-to-One  | Single     |

The weight tables are disconnected (no relationships) and are used purely for parameter selection.

---

## Design Philosophy

This model is intentionally lean and interactive:

- **No bi-directional filters** → Everything is clean and predictable  
- **Disconnected slicers** → Let you control logic without messing with relationships  
- **All logic in measures** → Virtually no calculated columns, no hidden cruft  
- **Custom-built sliders** → Gives you perfect control over weight values

> If you want to see how those weight values actually drive the score, head over to [Measures Overview](./measures_overview.md).
