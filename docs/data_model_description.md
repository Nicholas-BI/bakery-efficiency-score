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

## Weight Tables (Custom Slider Inputs)

These tables act like what-if parameters, but they aren’t created using Power BI’s built-in **Modeling > New Parameter** feature.

### Why not use standard What-If Parameters?

Because rounding errors near zero made them unreliable. You could select 0 and still get a tiny decimal like `1.11022e-16`, and that was enough to break the logic.

Here’s why that matters:  
The way the score works, every metric either ends up in the **numerator** (good) or the **denominator** (bad).  
So if you wanted to “turn off” a metric — say, you didn’t care about XP at all — you’d set the slider to zero and expect it to be skipped.

But if zero wasn’t *really* zero? It would sneak into the formula anyway, and suddenly your XP score is subtly messing with the rankings even though you said not to include it.

So I scrapped the default what-if method and built these tables by hand using `DATATABLE()`, which gave me full control over the values and formatting. That fixed the problem, kept logic clean, and made the sliders feel truly responsive.


### Example – `ProfitWeight`

```DAX
ProfitWeight = 
DATATABLE(
    "Profit Weight", DOUBLE,
    {
        {-4.0}, {-3.9}, {-3.8}, {-3.7}, {-3.6},
        {-3.5}, {-3.4}, {-3.3}, {-3.2}, {-3.1},
        {-3.0}, {-2.9}, {-2.8}, {-2.7}, {-2.6},
        {-2.5}, {-2.4}, {-2.3}, {-2.2}, {-2.1},
        {-2.0}, {-1.9}, {-1.8}, {-1.7}, {-1.6},
        {-1.5}, {-1.4}, {-1.3}, {-1.2}, {-1.1},
        {-1.0}, {-0.9}, {-0.8}, {-0.7}, {-0.6},
        {-0.5}, {-0.4}, {-0.3}, {-0.2}, {-0.1},
        { 0.0},
        { 0.1}, { 0.2}, { 0.3}, { 0.4}, { 0.5},
        { 0.6}, { 0.7}, { 0.8}, { 0.9}, { 1.0},
        { 1.1}, { 1.2}, { 1.3}, { 1.4}, { 1.5},
        { 1.6}, { 1.7}, { 1.8}, { 1.9}, { 2.0},
        { 2.1}, { 2.2}, { 2.3}, { 2.4}, { 2.5},
        { 2.6}, { 2.7}, { 2.8}, { 2.9}, { 3.0},
        { 3.1}, { 3.2}, { 3.3}, { 3.4}, { 3.5},
        { 3.6}, { 3.7}, { 3.8}, { 3.9}, { 4.0}
    }
)
```

This gives you perfect precision at 0, full control over the range, and no floating-point headaches.

The other weight tables — `CookTimeWeight`, `ServingsWeight`, and `XPWeight` — follow the same pattern.

Each one is disconnected from the model and accessed using `SELECTEDVALUE()` in DAX to feed into the score formula.

---

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
- **All logic in measures** → No calculated columns, no hidden cruft  
- **Custom-built sliders** → Gives you perfect control over weight values

> If you want to see how those weight values actually drive the score, head over to [Measures Overview](./measures_description.md).
