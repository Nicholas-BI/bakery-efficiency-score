# Visuals Description

The Bakery Story dashboard is a single-page Power BI report (with tooltip and drillthrough support) built to help players make smarter, faster baking decisions. Every visual on the page responds dynamically to your custom preferences, whether you're chasing fast cash, XP, or chill, low-maintenance batches.

It’s clean, interactive, and a little nerdy — just how we like it.

---

## 🧁 Main View

This is the heart of the report. It’s where you explore recipe efficiency based on what *you* care about.

### Layout Overview

| Region         | Contents |
|----------------|----------|
| **Top Left**   | Best Recipe display — or a message if weights need adjusting |
| **Top Center** | Appliance selector (multi-select dropdown) |
| **Top Right**  | Weight sliders and preset bookmark buttons |
| **Middle**     | Column chart: Efficiency Score by Recipe |
| **Right Panel**| Slicers for cook time, profit, XP, etc. |

### Core Visuals

- **Bar Chart: Efficiency Score by Recipe**  
  - Each bar is a recipe, sorted by score  
  - Scores update in real time as you change weights  
  - Hovering shows a tooltip breakdown (see below!)

- **Best Recipe Card**  
  - Shows the top-ranked recipe unless all weights are zero or a selection is active  
  - Message updates dynamically based on report context

- **Slider Panel (Disconnected Slicers)**  
  - Profit, Cook Time, Servings, XP  
  - Each slider adjusts how important the metric is (–4 to +4)  
  - These weights are used as **exponents** in the scoring formula  
  - 0 means “don’t care,” negative means “penalize”

- **Cook Time Range Selector**  
  - A numeric range slicer to limit the recipe pool  
  - Helps you say “just show me things that take around 4 hours,” etc.

- **Appliance Filter**  
  - Multi-select list of every appliance in the game  
  - Only see what’s cookable with your current setup

- **Bookmark Buttons (Hearts!)**  
  - Quick toggle between playstyles:
    - Balanced
    - Quick Cash
    - XP Farm
    - Party Host
    - Reset to neutral weights  
  - CTRL+Click is required (Power BI behavior)

---

## 🪄 Tooltip Panel (Hover Preview)

When you hover over a bar in the main chart, you’ll see a pop-up showing the “why” behind that recipe’s score.

This tooltip includes:

| Field                | Description |
|---------------------|-------------|
| **Efficiency Score** | Final result after all weights applied |
| **Total Profit**     | Raw profit before normalization |
| **Normalized Profit**| Value scaled relative to other recipes |
| **Total Cook Minutes** | How long it takes, end-to-end |
| **Normalized Cook Time** | Scaled cook time |
| **Total Servings**   | How many dishes it produces |
| **Normalized Servings** | Scaled servings |
| **Total XP**         | Experience gained |
| **Normalized XP**    | Scaled XP value |

The tooltip helps users understand what’s boosting or dragging each score — without leaving the chart. It’s especially useful when weights are extreme and the chart shifts dramatically.

> Think of it like a recipe résumé: here’s why this one ranks how it does.

---

## 🔎 Drillthrough Page (Deep Dive)

This is where you can **zoom in** on a single recipe after clicking it in the main chart.

Once a recipe is selected, the drillthrough page shows:

| Insight | Description |
|--------|-------------|
| **Profit per Minute** | Speed-to-income ratio — how fast does this earn? |
| **XP per Minute** | How much leveling juice you get per hour |
| **Servings per Minute** | Tells you how quickly a batch clears out |
| **Profit per Serving** | What each plate is worth |
| **XP per Serving** | Bonus points per customer served |
| **Total Stats** | Raw numbers for profit, servings, XP, cook time |
| **Normalized Stats** | The same values scaled between 0 and 1 for fair comparison |

Planned visuals:

- Small KPI cards for each of the per-minute/per-serving ratios  
- A radar chart showing relative strengths across Profit, Time, XP, and Servings  
- A visual indicator of how close this recipe is to the “best fit” based on your weights

> This page is all about context. You found a top recipe — now let’s explore *why* it works, and how it stacks up in every category.

---

## ✨ Design Highlights

- Heart-shaped buttons for bookmarks because... well, bakery ❤️  
- Clean, consistent layout keeps the scoring logic front and center  
- Tooltip and drillthrough make the report *feel* like a game — click, hover, explore  
- Normalized metrics ensure apples-to-apples comparison, no matter the scale  
- Weight sliders offer real control: it’s not just “turn up profit,” it’s *how much* you care about it

---

## Screenshot Reference

| Main View | Tooltip Panel | Drillthrough (Planned) |
|-----------|----------------|-------------------------|
| ![Main View](../images/pages/ranked_recipes.png) | ![Tooltip Panel](../images/pages/tooltip_table.png) | *(Coming soon)* |

---

## Want to Learn More?

Check out [measures_description.md](./measures_description.md) to see how the scoring logic actually works — all the DAX behind the curtain.

---

This isn’t just a dashboard. It’s a bakery simulator. A recipe optimizer. A choose-your-own-playstyle engine. And it all fits on one page.

