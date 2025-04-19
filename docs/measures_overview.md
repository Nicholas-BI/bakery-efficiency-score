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

---

## ⚖️ Step 2: Normalize Metrics (into [1 → 2] range)

To fairly compare metrics that live on different scales (e.g., profit might be in the 1000s, XP in the 10s), we normalize each into a consistent range.

### 🎯 Goal:
Convert every metric to a **unitless, comparable number between 1 and 2**, using:

```
Normalized Value = 1 + (This Recipe's Total / Max Total in Context)
```

If a specific **appliance** is selected, we normalize within that group.  
If not, we normalize against the global maximum.

This results in:
- `[Normalized Profit]`
- `[Normalized Cook Minutes]`
- `[Normalized Servings]`
- `[Normalized XP]`

---

## 🎛️ Step 3: Player-Controlled Weighting (via Exponents)

Each metric is assigned a **player-defined weight** (via slicers), ranging from -2 to 2.

### What the weight means:
- **Positive Weight:** "I want *more* of this" → Goes in the **numerator**
- **Negative Weight:** "I want *less* of this" → Goes in the **denominator**
- **Zero Weight:** "I don’t care" → Treated as 1 (neutral)

This turns a multi-objective optimization problem into a **multiplicative scoring model**:

```
Score = (P^p * C^c * S^s * X^x) / (P^-p * C^-c * S^-s * X^-x)
```

Where:
- `P` = Normalized Profit  
- `p` = profit weight  
- `C`, `S`, `X` = other normalized metrics  
- Negative exponents shift the metric into the denominator

---

## 🚀 Step 4: Efficiency Score Formula

Here’s the complete DAX implementation of the Efficiency Score logic:

```DAX
Efficiency Score (Filtered) = 
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

VAR BaseResult = DIVIDE( Numerator, Denominator, 0 )

VAR HasRows = COUNTROWS( Fact_Bakery )
RETURN
    IF( HasRows = 0, BLANK(), BaseResult )
```

This is the core of the ranking engine—**a balanced ratio** of weighted priorities, dynamically computed per recipe and context.

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
