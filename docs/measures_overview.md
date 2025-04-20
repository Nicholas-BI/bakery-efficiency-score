# 📊 Measures Overview

This document explains how the **Bakery Story Efficiency Score** works from concept to implementation. The report ranks bakery recipes based on what *you* care about—Profit, Cook Time, Servings, and XP—by letting you assign custom weights. The scoring logic is flexible, explainable, and fully dynamic.

We’ll focus on **how it works**, not just what the measures are.

---

## Step 1: Start With Raw Totals

Each recipe begins with four basic totals:
- Total Cook Minutes
- Total Servings
- Total Profit
- Total XP

These are calculated using simple `SUM` logic over the fact table:

```DAX
Total Income = SUM(Fact_Bakery[Income])
Total Cost   = SUM(Fact_Bakery[Cost])
Total Profit = [Total Income] - [Total Cost]
Total Cook Minutes = SUM(Fact_Bakery[Minutes])
Total Servings     = SUM(Fact_Bakery[Servings])
Total XP           = SUM(Fact_Bakery[XP])
```

---

## Step 2: Normalize the Metrics

Each metric is normalized using ratio scaling, shifted up by `+1` to keep results within the `[1 → 2]` range. This avoids divide-by-zero errors and ensures relative comparisons across different units (minutes, dollars, etc.).

The general form is:

> `Normalized = 1 + (This Value ÷ Max Value)`

The `Max Value` is context-sensitive:
- If you're viewing a specific **appliance**, it uses the max value *within that appliance*
- Otherwise, it falls back to the global maximum

Example for Cook Minutes:

```DAX
Normalized Cook Minutes = 
VAR ThisTotal =
    [Total Cook Minutes]

VAR MaxTotalAll =
    MAXX(
        ALL( Dim_Recipe[Recipe] ),
        [Total Cook Minutes]
    )

VAR MaxTotalAppl =
    MAXX(
        ALL( Dim_Appliance[Appliance] ),
        [Total Cook Minutes]
    )

VAR Denominator =
    IF(
        HASONEVALUE( Dim_Appliance[Appliance] ),
        MaxTotalAppl,
        MaxTotalAll
    )

RETURN
    1 + DIVIDE( ThisTotal, Denominator, 0 )
```

You’ll repeat this pattern for:
- `Normalized Profit`
- `Normalized Servings`
- `Normalized XP`

---

## Step 3: Apply Player Weights

Players use slicers to assign custom weights (from -20 to +20) to each metric:

- Positive weights = you want **more** of something → boosts the score
- Negative weights = you want **less** of something → lowers the score
- Zero weights = you **don’t care** about that metric

---

## Step 4: Build the Score

The normalized metrics are raised to the power of their weights. Positive-weighted metrics go into the numerator; negative ones go into the denominator.

```DAX
Efficiency Score = 
VAR PW = SELECTEDVALUE( ProfitWeight[Profit Weight],      0 )
VAR CW = SELECTEDVALUE( CookTimeWeight[Cook Time Weight], 0 )
VAR SW = SELECTEDVALUE( ServingsWeight[Servings Weight],  0 )
VAR XW = SELECTEDVALUE( XPWeight[XP Weight],              0 )

VAR ProfitBase = [Normalized Profit]
VAR CookBase   = [Normalized Cook Minutes]
VAR ServeBase  = [Normalized Servings]
VAR XPBase     = [Normalized XP]

VAR Numerator =
    IF( PW > 0, POWER( ProfitBase, PW ), 1 ) *
    IF( CW > 0, POWER( CookBase,   CW ), 1 ) *
    IF( SW > 0, POWER( ServeBase,  SW ), 1 ) *
    IF( XW > 0, POWER( XPBase,     XW ), 1 )

VAR Denominator =
    IF( PW < 0, POWER( ProfitBase,  -PW ), 1 ) *
    IF( CW < 0, POWER( CookBase,    -CW ), 1 ) *
    IF( SW < 0, POWER( ServeBase,   -SW ), 1 ) *
    IF( XW < 0, POWER( XPBase,      -XW ), 1 )

VAR RawScore = DIVIDE( Numerator, Denominator, 0 )

VAR HasData = COUNTROWS( Fact_Bakery ) > 0

VAR RecipeScore =
    IF( HasData, RawScore, BLANK() )

RETURN
IF(
    ISINSCOPE( Dim_Recipe[Recipe] ),
    RecipeScore,
    MAXX(
        VALUES( Dim_Recipe[Recipe] ),
        RecipeScore
    )
)
```

This formula dynamically evaluates each recipe’s alignment with your chosen strategy.

---

## Step 5: Find the Best Recipe

Once every recipe has a score, we find the top-ranked one (with tiebreakers and error handling):

```DAX
Best Recipe = 
VAR Recipes =
    FILTER(
        VALUES(Dim_Recipe[Recipe]),
        NOT ISBLANK([Efficiency Score])
    )

VAR ScoreMax =
    MAXX(Recipes, [Efficiency Score])

VAR TopRecipes =
    FILTER(
        Recipes,
        [Efficiency Score] = ScoreMax
    )

RETURN
IF(
    COUNTROWS(Recipes) < 2
        || MINX(Recipes, [Efficiency Score]) = ScoreMax,
    "Adjust weights or deselect recipe",
    CONCATENATEX(
        TopRecipes,
        Dim_Recipe[Recipe],
        ", "
    )
)
```

---

## Summary of the Logic

1. **Calculate raw totals** (profit, cook time, etc.)
2. **Normalize** each metric between 1–2
3. **Apply weights** from user input
4. **Score each recipe** using exponent math
5. **Return the best** based on your preferences

All logic is filter-aware, bookmark-compatible, and built entirely in DAX.

---

## Future Features

- Incorporate appliance usage costs (opportunity cost logic)
- Add tornado charts to visualize impact of each weight
- Add appliance-recipe combo recommendations

---

Want to try it yourself?  
👉 **[Download the .pbix file](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/bakery_story.pbix)**  
👉 **[Download the DAX measures](https://raw.githubusercontent.com/Nicholas-BI/bakery-efficiency-score/main/docs/dax_measures.xlsx)**
