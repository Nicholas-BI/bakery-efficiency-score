# 📊 Measures Overview

This document details all DAX measures powering the **Bakery Story Efficiency Score** dashboard. You’ll find base aggregations, normalized ratios, weight handling, scoring logic, and ranking formulas.

---

## 🧮 Base Aggregations

Core sum and arithmetic measures that feed into the normalization logic.

-- Total Cook Minutes
Total Cook Minutes =
    SUM(Fact_Bakery[Minutes])

-- Total Servings
Total Servings =
    SUM(Fact_Bakery[Servings])

-- Total Income
Total Income =
    SUM(Fact_Bakery[Income])

-- Total Cost
Total Cost =
    CALCULATE(SUM(Fact_Bakery[Cost]))

-- Total Profit
Total Profit =
    [Total Income] - [Total Cost]

-- Total XP
Total XP =
    SUM(Fact_Bakery[XP])

---

## ⚖️ Normalized Metrics

Each metric is scaled into the range [1 → 2], context‑aware by appliance or global maxima.

-- Normalized Profit
Normalized Profit =
    VAR ThisTotal = [Total Profit]
    VAR MaxTotalAll = MAXX(ALL(Dim_Recipe[Recipe]), [Total Profit])
    VAR MaxTotalAppl = MAXX(ALL(Dim_Appliance[Appliance]), [Total Profit])
    VAR Denominator =
        IF(HASONEVALUE(Dim_Appliance[Appliance]), MaxTotalAppl, MaxTotalAll)
    RETURN 1 + DIVIDE(ThisTotal, Denominator, 0)

-- Normalized XP
Normalized XP =
    VAR ThisTotal = [Total XP]
    VAR MaxTotalAll = MAXX(ALL(Dim_Recipe[Recipe]), [Total XP])
    VAR MaxTotalAppl = MAXX(ALL(Dim_Appliance[Appliance]), [Total XP])
    VAR Denominator =
        IF(HASONEVALUE(Dim_Appliance[Appliance]), MaxTotalAppl, MaxTotalAll)
    RETURN 1 + DIVIDE(ThisTotal, Denominator, 0)

-- Normalized Cook Minutes
Normalized Cook Minutes =
    VAR ThisTotal = [Total Cook Minutes]
    VAR MaxTotalAll = MAXX(ALL(Dim_Recipe[Recipe]), [Total Cook Minutes])
    VAR MaxTotalAppl = MAXX(ALL(Dim_Appliance[Appliance]), [Total Cook Minutes])
    VAR Denominator =
        IF(HASONEVALUE(Dim_Appliance[Appliance]), MaxTotalAppl, MaxTotalAll)
    RETURN 1 + DIVIDE(ThisTotal, Denominator, 0)

-- Normalized Servings
Normalized Servings =
    VAR ThisTotal = [Total Servings]
    VAR MaxTotalAll = MAXX(ALL(Dim_Recipe[Recipe]), [Total Servings])
    VAR MaxTotalAppl = MAXX(ALL(Dim_Appliance[Appliance]), [Total Servings])
    VAR Denominator =
        IF(HASONEVALUE(Dim_Appliance[Appliance]), MaxTotalAppl, MaxTotalAll)
    RETURN 1 + DIVIDE(ThisTotal, Denominator, 0)

---

## 🎚️ Parameter & Selector Measures

-- Normalized Value
Normalized Value =
    SWITCH(
        SELECTEDVALUE(Metrics[Metric]),
        "Profit", [Normalized Profit],
        "Cook Time", [Normalized Cook Minutes],
        "Servings", [Normalized Servings],
        "XP", [Normalized XP],
        BLANK()
    )

-- Selected Weight (Exponent)
Selected Weight (Exponent) =
    SWITCH(
        SELECTEDVALUE(Metrics[Metric]),
        "Profit", SELECTEDVALUE(ProfitWeight[Profit Weight], 0),
        "Cook Time", SELECTEDVALUE(CookTimeWeight[Cook Time Weight], 0),
        "Servings", SELECTEDVALUE(ServingsWeight[Servings Weight], 0),
        "XP", SELECTEDVALUE(XPWeight[XP Weight], 0),
        0
    )

-- Placement
Placement =
    VAR w = [Selected Weight (Exponent)]
    RETURN
        SWITCH(
            TRUE(),
            w > 0, "Numerator",
            w < 0, "Denominator",
            "Ignored"
        )

-- Contribution
Contribution =
    VAR w = [Selected Weight (Exponent)]
    VAR v = [Normalized Value]
    RETURN
        SWITCH(
            TRUE(),
            w = 0, 1,
            POWER(v, ABS(w))
        )

---

## 🚀 Scoring Logic

-- Efficiency Score (Filtered)
Efficiency Score (Filtered) =
    VAR PW = SELECTEDVALUE(ProfitWeight[Profit Weight], 0)
    VAR CW = SELECTEDVALUE(CookTimeWeight[Cook Time Weight], 0)
    VAR SW = SELECTEDVALUE(ServingsWeight[Servings Weight], 0)
    VAR XW = SELECTEDVALUE(XPWeight[XP Weight], 0)
    VAR ProfitBase = [Normalized Profit]
    VAR CookBase = [Normalized Cook Minutes]
    VAR ServeBase = [Normalized Servings]
    VAR XPBase = [Normalized XP]
    VAR Numerator =
        IF(PW > 0, POWER(ProfitBase, PW), 1) *
        IF(CW > 0, POWER(CookBase, CW), 1) *
        IF(SW > 0, POWER(ServeBase, SW), 1) *
        IF(XW > 0, POWER(XPBase, XW), 1)
    VAR Denominator =
        IF(PW < 0, POWER(ProfitBase, -PW), 1) *
        IF(CW < 0, POWER(CookBase, -CW), 1) *
        IF(SW < 0, POWER(ServeBase, -SW), 1) *
        IF(XW < 0, POWER(XPBase, -XW), 1)
    VAR BaseResult = DIVIDE(Numerator, Denominator, 0)
    VAR HasRows = COUNTROWS(Fact_Bakery)
    RETURN IF(HasRows = 0, BLANK(), BaseResult)

-- Best Recipe (By Efficiency)
Best Recipe (By Efficiency) =
    VAR Candidates =
        FILTER(
            VALUES(Dim_Recipe[Recipe]),
            NOT ISBLANK([Efficiency Score (Filtered)])
        )
    VAR CountCand = COUNTROWS(Candidates)
    VAR ScoresTable =
        ADDCOLUMNS(
            Candidates,
            "Score", [Efficiency Score (Filtered)]
        )
    VAR MinScore = MINX(ScoresTable, [Score])
    VAR MaxScore = MAXX(ScoresTable, [Score])
    VAR TopRecipe =
        MAXX(
            TOPN(1, ScoresTable, [Score], DESC),
            Dim_Recipe[Recipe]
        )
    RETURN
        IF(
            CountCand < 2 || MinScore = MaxScore,
            "Adjust weights or deselect recipe",
            TopRecipe
        )
"""

# Define output file path
output_path = Path("/mnt/data/measures_overview.txt")

# Write the content to the file
output_path.write_text(dax_measures_content)

# Return the file path for download
output_path.name
