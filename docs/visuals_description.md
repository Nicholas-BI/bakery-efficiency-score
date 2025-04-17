# Visuals Description

This Power BI report is a single-page, fully interactive recipe ranking engine. It’s built for *Bakery Story* players who want to squeeze the most out of their time and ovens — whether that means big profits, lots of XP, or zero babysitting.

The layout is intentionally simple but packed with control — so even though it's just one page, it adapts like a chameleon based on your preferences.

---

## 🔧 Slicers & Filters

The core of the experience is interactivity. Every filter and selector directly reshapes the rankings based on what *you* care about:

### 🎚 Weight Sliders (Profit, Cook Time, Servings, XP)
- These are the *heart* of the report
- Change how much each metric affects the final score
- Built using a custom table system (not traditional What-If parameters) to avoid floating-point weirdness
- Sliders drive exponent-based logic: higher weights = stronger impact

### 🧁 Appliance Selector
- Lets you filter to just the appliances you own (deep fryer gang rise up)
- Helps you narrow the field to what’s actually cookable

### ⏲ Cook Time Range
- Want to cook something while you’re gone for 3 hours?
- This slider helps you filter by real-world time so you’re not stuck serving a 12-hour cake for no reason

---

## ❤️ Preset Buttons (CTRL+Click)

Custom bookmark buttons shaped like candy hearts 💖

Each one represents a *playstyle preset*, instantly setting the weights for a particular strategy:

- **Quick Cash** – Fast, profitable, small batches  
- **XP Farm** – Maximize experience gain  
- **Party Host** – Big batches, no stress  
- **Balanced** – A little bit of everything  
- **Reset** – Clears all slicers and brings things back to neutral

You can CTRL+Click to activate one — the hearts pulse a little when clicked for fun (and clarity).

---

## 📊 Recipe Rankings Chart

Main bar chart that shows the **Efficiency Score** for every recipe based on your current settings.

- Always normalized from 0 to 1  
- Updates instantly when you change weights or slicers  
- Sorts from best to worst (or ties if everything’s equal)  
- Hover to get a detailed breakdown of how that recipe’s score was calculated

The tooltip is especially handy — it shows each metric’s normalized value, where it was used (numerator or denominator), and how much it contributed to the final score. It’s like peeking under the hood.

---

## 🧠 Best Recipe Card

This card dynamically shows:

- The **top recipe** given your current settings  
- A fallback message ("Adjust weights or deselect recipe") when all recipes score the same or if you have a slicer selection active

This visual helps answer the question:  
> "If I only bake *one* thing right now, what should it be?"

---

## ✨ Design Touches

- Minimalist white space layout for clarity
- Bold visual hierarchy: chart, slicers, score → in that order
- Hover tooltips provide deep logic without cluttering the UI
- Button and slicer layout is grouped for ergonomic control

---

## Screenshot Reference

| Main View | Weight Sliders & Presets |
|-----------|--------------------------|
| ![Main View](../images/pages/ranked_recipes.png) | ![Presets and Sliders](../images/pages/sliders_and_bookmarks.png) |

---

## Purpose

This report page is all about **reactivity**. You tell it what matters — it ranks accordingly. There are no hard-coded values, no assumptions about what’s “best.” It’s a score engine wrapped in candy-colored visuals.

If you’re curious how it all works under the hood, check out:  
👉 [measures_description.md](./measures_description.md)
