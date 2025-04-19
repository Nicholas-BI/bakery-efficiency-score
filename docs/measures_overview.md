# 📊 Efficiency Scoring System – Conceptual Overview

This document walks through the **mathematical logic** and **Power BI implementation** behind the **Bakery Story Efficiency Score** model. It’s designed to rank in-game recipes based on player preferences—Profit, Cook Time, Servings, and XP—through a dynamic, weighted scoring system.

Rather than listing every measure, this guide explains how they work together conceptually, using algebra, DAX, and plain English.

---

## 🧮 Step 1: Raw Totals

We begin by calculating **base metrics** for each recipe:  
- `Profit = Income - Cost`  
- `Cook Time = Minutes required`  
- `Servings = How many customers can consume it`  
- `XP = Experience gained`

These are simple `SUM` aggregations on the fact table (`Fact_Bakery`), grouped by recipe.

```DAX
-- Example: Total Profit
Total Profit =
    [Total Income] - [Total Cost]
```

---

## ⚖️ Step 2: Normalize Metrics (into [1 → 2] range)

To fairly compare metrics that live on different scales (e.g., profit might be in the 1000s, XP in the 10s), we normalize each into a consistent range.

### 🎯 Goal:
Convert every metric to a **unitless, comparable number between 1 and 2**, using:

```
Normalized Value = 1 + (This Recipe's Total / Max Total in Context)
```

- If a specific **appliance** is selected, we normalize within that group.
- If not, we normalize against the global maximum.

```DAX
Normalized Profit =
    VAR ThisTotal = [Total Profit]
    VAR MaxAll = MAXX(ALL(Dim_Recipe[Recipe]), [Total Profit])
    VAR MaxAppliance = MAXX(ALL(Dim_Appliance[Appliance]), [Total Profit])
    VAR Denominator =
        IF(HASONEVALUE(Dim_Appliance[Appliance]), MaxAppliance, MaxAll)
    RETURN 1 + DIVIDE(ThisTotal, Denominator, 0)
```

This gives us four normalized inputs: `[Normalized Profit]`, `[Normalized Cook Minutes]`, `[Normalized Servings]`, and `[Normalized XP]`.

---

## 🎛️ Step 3: Player-Controlled Weighting (via Exponents)

Each metric is assigned a **player-defined weight** (via slicers), ranging from -2 to 2.

### What the weight means:
- **Positive Weight:** "I want *more* of this" → Goes in the **numerator**
- **Negative Weight:** "I want *less* of this" → Goes in the **denominator**
- **Zero Weight:** "I don’t care" → Neutralized (becomes 1)

### Algebraically:
```
Score = (P^p) * (C^c) * (S^s) * (X^x)
```
Where:
- `P` = Normalized Profit  
- `p` = profit weight  
- `C`, `S`, `X` = other normalized metrics  
- Negative exponents push metrics into the denominator.

```DAX
-- Contribution for a single metric
Contribution =
    VAR w = [Selected Weight (Exponent)]
    VAR v = [Normalized Value]
    RETURN
        SWITCH(
            TRUE(),
            w = 0, 1,
            POWER(v, ABS(w))
        )
```

---

## 🧮 Step 4: Score Calculation

Using all four metrics and their weights, we build a final formula:

```DAX
Efficiency Score =
    (P^p * C^c * S^s * X^x) / (P^-p * C^-c * S^-s * X^-x)
```

This is implemented in DAX as a numerator and denominator, where each metric is conditionally included based on the sign of its weight:

```DAX
-- Conceptual structure
Numerator =
    IF(p > 0, P^p, 1) *
    IF(c > 0, C^c, 1) *
    ...

Denominator =
    IF(p < 0, P^-p, 1) *
    IF(c < 0, C^-c, 1) *
    ...
```

If the denominator is 1, all weights are positive (maximize all).
If the numerator is 1, all weights are negative (minimize all).
Zero weights are treated as neutral and do not affect the outcome.

---

## 🥇 Step 5: Rank & Display

Once each recipe has a calculated **Efficiency Score**, we identify the best option in the current filter context.

- Filter out recipes with no valid score
- Rank them descending
- Show the top result
- If there's a tie or not enough data, display a fallback message

```DAX
Best Recipe =
    VAR Candidates = FILTER(VALUES(...), NOT ISBLANK([Efficiency Score]))
    ...
    RETURN IF(TooFewOptions || NoScoreDifference, "Adjust weights", TopRecipe)
```

---

## ✅ Summary of the Flow

1. **Aggregate raw metrics** from the fact table  
2. **Normalize** each to [1 → 2] using max-based scaling  
3. **Apply player weights** using exponent math  
4. **Calculate a combined score** (numerator / denominator)  
5. **Identify the best recipe** in context

This model allows flexible, personalized optimization—whether you value XP grinding, bulk batches, rapid turnaround, or raw profit.

---

## 🛠️ Future Improvements

- Multi-appliance optimization logic  
- Visual sensitivity analysis (e.g., tornado charts)  
- Prebuilt bookmarks for common profiles like "XP Farmer" or "Passive Player"  
- Appliance utilization costs (opportunity cost modeling)

---

Want to try it yourself?  
👉 **[Click here to download the .pbix file](./BakeryStory_Efficiency.pbix)**  
👉 **[Click here to download the DAX measures](./docs/dax_measures.xlsx)**
