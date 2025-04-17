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

These disconnected tables store slider values the user selects to influence the scoring formula. Each one represents a trait you can prioritize.

### `ProfitWeight`
- Contains values from –4 to +4 (e.g., –2.0, 0, 2.5, etc.)
- Positive weight boosts high-profit recipes
- Negative weight punishes high-profit recipes (rare, but supported!)

### `CookTimeWeight`
- Positive values prefer long bakes (for idle play)
- Negative values prefer fast bakes (for fast turnarounds)

### `ServingsWeight`
- Positive values reward large batches (good for low-touch play)
- Negative values punish them (delays payout)

### `XPWeight`
- Prioritizes XP gain from completed dishes

---

## Measure Table

### `Measure Table`
- Dummy table used to hold display measures (e.g., top recipe label)
- Doesn’t connect to anything — just here to keep things tidy

---

## Relationship Summary

| From                 | To                | Type         | Direction |
|----------------------|-------------------|--------------|-----------|
| `Fact_Bakery[Recipe]`   | `Dim_Recipe[Recipe Name]` | Many-to-One | Single     |
| `Fact_Bakery[Appliance]` | `Dim_Appliance[ApplianceName]` | Many-to-One | Single     |

All relationships are single-directional. The weight tables are disconnected and used via `SELECTEDVALUE()` to drive scoring logic dynamically.

---

## Design Philosophy

This model is intentionally lean:

- **No bi-directional filters**  
  Keeps things simple, fast, and predictable

- **Disconnected slicers for logic injection**  
  Slider values are passed to DAX using `SELECTEDVALUE()` and used as exponents

- **No calculated columns**  
  All transformations (e.g., normalized values, weighted scores) are done via measures

This setup makes the report feel interactive and snappy while keeping the backend clean and efficient.

If you want to see how those weight values flow into the scoring formula, head over to [Measures Overview](./measures_description.md).
