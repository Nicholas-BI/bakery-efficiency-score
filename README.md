# 📊 Bakery Story: Recipe Efficiency Dashboard (Power BI)

A Power BI dashboard for *Bakery Story* players to optimize baking decisions—whether you’re targeting quick revenue, high XP, or efficient workflows. Customize sliders for **Profit**, **Cook Time**, **Servings**, and **XP**, and watch the rankings adapt in real time.

---

## 💡 Purpose

This dashboard was born from a simple question:  
> Instead of prescribing the “best” bake, what if **you** could decide which metrics matter and see the results instantly?

---

## 🛠️ Features

- **📊 Dynamic Ranking**  
  Recipes are ranked instantly based on your weight selections.  
- **🎛️ Slider Controls**  
  Adjust Profit, Cook Time, Servings, and XP to fine-tune your priorities.  
- **⚖️ Exponent‑Based Scoring**  
  Non‑linear weighting ensures heavier preferences have greater impact.  
- **🔎 Advanced Filtering**  
  Filter by appliance (oven, fryer, drink machine) or cook‑time window.  
- **🔘 Preset Strategies**  
  One‑click presets like “Quick Cash” and “XP Farm.”  
- **📈 Interactive Tooltips**  
  See the exact calculation behind each recipe’s score.  
- **🔢 Fair Normalization**  
  Ratios ensure all attributes—regardless of units—are compared equitably.

---

## 📁 Repo Structure

    /
    ├─ README.md
    ├─ docs/
    │   ├─ measures_description.md    ← Scoring logic deep dive
    │   └─ visuals_description.md     ← Dashboard walkthrough
    ├─ power_query/                   ← M code for data prep
    ├─ images/
    │   ├─ pages/                     ← Screenshots
    │   └─ diagrams/                  ← Dependency & flow charts
    ├─ dax_measures.xlsx              ← All DAX measures
    └─ LICENSE                        ← CC BY‑NC 4.0

---

## 🔍 Scoring Logic

| Attribute     | Description                                     |
|---------------|-------------------------------------------------|
| **Profit**    | Revenue minus ingredient cost                   |
| **Cook Time** | Minutes required (delays final payout)          |
| **Servings**  | Portions produced (last serving triggers revenue) |
| **XP**        | Experience points gained                        |

1. **Normalize** each metric as a ratio  
2. **Raise** to the power of its slider value  
3. **Combine**—positives multiply, negatives divide  
4. **Rank** by final score  

> Full formula details in [Measures Overview](./docs/measures_description.md).

---

## 🎯 Example Playstyles (Presets)

| Strategy     | Profit | Cook Time | Servings | XP | Notes                               |
|--------------|--------|-----------|----------|----|-------------------------------------|
| Quick Cash   | 4      | –4        | –2       | 1  | Maximize revenue, minimize delays   |
| XP Farm      | 1      | –2        | –2       | 4  | Prioritize XP, avoid long bakes     |
| Party Host   | 1      | –2        | 4        | 0  | Serve large batches for events      |
| Balanced     | 2      | –2        | 1        | 1  | Even distribution across metrics    |

---

## 📷 Screenshots

| Main View                                          | Sliders & Presets                                    |
|----------------------------------------------------|------------------------------------------------------|
| ![Ranked Recipes](./images/pages/ranked_recipes.png) | ![Controls](./images/pages/sliders_and_bookmarks.png) |

---

## 🚀 Getting Started

1. **Clone** this repository  
2. **Open** `BakeryStory_Efficiency.pbix` with Power BI Desktop  
3. **Adjust** the sliders to your preferred weights  
4. **Explore** the ranked recipes and hover for details  

> Download Power BI Desktop: https://powerbi.microsoft.com/desktop/

---

## 🔐 License

Licensed under [CC BY‑NC 4.0](./LICENSE).  
Feel free to share, adapt, and remix for personal or community use—commercial use requires permission.

---

## 📣 Contributing

Questions, feedback, or custom presets? Open an issue or submit a PR—let’s make this tool even better!
