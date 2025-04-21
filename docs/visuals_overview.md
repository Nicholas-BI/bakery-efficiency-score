# 🎨 Visuals Overview

This single-page Power BI report helps *Bakery Story* players bake smarter, not harder. Every visual responds in real time to your slider settings—whether you're chasing fast XP, quick profit, or low-effort bakes.

---

## 🧭 Main View Overview

This is the heart of the report—where recipes rise or fall based on what *you* value.

| Region         | Contents                                                                 |
|----------------|--------------------------------------------------------------------------|
| **Top Left**   | **Axis Field Selector** – toggles chart axis between Appliance or Recipe |
| **Top Center** | **Best Recipe Card** – displays the top result (or tie/neutral message)  |
| **Top Right**  | **Appliance Selector** and **Cook Time Range** slicer                    |
| **Left Panel** | **Preset Buttons** – Reset, Quick Cash, XP Farm, Party Host, Balanced *(CTRL+Click if not published)* |
| **Center**     | **Efficiency Bar Chart** – real-time ranking of recipes                  |
| **Right Panel**| **Weight Sliders** – Profit, Cook Time, Servings, XP (–20 to +20)        |

---

## 📊 Key Visuals

### Efficiency Bar Chart
- Ranks recipes by real-time score  
- Fully dynamic and filter-aware  
- Hover reveals score breakdown (see tooltip section)

### Best Recipe Card
- Displays the highest-ranked recipe  
- Handles ties or neutral scores with fallback messaging  
- Updates live with every change in weights or filters

### Weight Sliders (Disconnected Slicers)
- Adjust scoring weight for each trait (–20 to +20)  
- Values are applied as **exponents** in the scoring formula  
- `0` = neutral, negatives penalize, positives boost

### Cook Time Filter
- Restrict visible recipes by total cook time (e.g., 30–120 minutes)

### Appliance Filter
- Filter by appliances you own—hide recipes you can’t make yet

### Bookmark Buttons
- Toggle preset strategies:
  - **Balanced**  
  - **Quick Cash**  
  - **XP Farm**  
  - **Party Host**  
  - **Reset**

---

## 🪄 Tooltip (Hover Breakdown)

Hovering over any bar reveals the underlying logic behind each score.

| Field            | Description                                     |
|------------------|-------------------------------------------------|
| **Metric**       | The trait being weighed (Profit, XP, etc.)      |
| **Normalized**   | The [1–2] range version of that value           |
| **Weight Applied** | Slider value used as an exponent               |
| **Placement**    | Whether used in the numerator, denominator, or ignored |
| **Contribution** | The final value contributing to the score       |

---

## 🖌️ Design Touches

- Heart-shaped bookmark buttons for playful UI
- Weight logic handled entirely with **exponents**, not raw multipliers
- Tooltips make the scoring transparent and intuitive
- Normalized metrics ensure fair comparisons across all values
- One layout, infinite playstyles

---

## 🖼️ Screenshot

![Bakery Story Screenshot](./images/pages/bakery_story.png)

---

## 📚 More Info

Curious how the scoring works?

📄 [See Measures Overview](./measures_overview.md) for the full DAX breakdown.

This isn’t just a dashboard—it’s a **recipe optimizer and strategy engine**, all in one scrollable screen.
