# 🍰 Bakery Story: Recipe Efficiency Dashboard (Power BI)

This is a Power BI dashboard for *Bakery Story* players who want to make smarter decisions about what to cook — whether you're after fast cash, big XP, or low-maintenance bakes. It ranks recipes based on **what *you* care about**, using a custom scoring system that reacts to sliders for **Profit**, **Cook Time**, **Servings**, and **XP**.

> It’s a mix of math, game logic, and a dash of obsessive nerding-out.

---

## 👋 Why I Made This

This started with a friendly disagreement between me and my partner, Stephanie.

She saw big-serving dishes as a good thing — fewer check-ins, more chill.  
I saw them as a delay — you don’t get paid until the *last* serving is eaten, and I wanted profit *fast*.

We were both right. It just depended on what you’re optimizing for.

That was the lightbulb moment:  
> What if the report didn't decide what was "best"?  
> What if it let **you** decide what's important, and then adjusted the rankings *dynamically*?

And so this dashboard was born.

---

## 🧭 What It Does

- 📊 **Ranks every recipe** based on your personal goals  
- 🎚️ **Slider controls** let you weigh Profit, Cook Time, Servings, and XP — the score updates in real time  
- 🧮 **Exponent-based logic** means higher weights have more impact (it's not just linear)  
- 🍳 **Filter by appliance** — see only what you can cook on your ovens, deep fryers, or drink machines  
- ⏲️ **Filter by cook time** — want to prep something while you’re gone for 4 hours? Just pick that time range and see your best options  
- 🔁 **Preset buttons** let you switch between playstyles like “Quick Cash” and “XP Farm”  
- 🔍 Hover over any recipe to see a detailed **tooltip breakdown** showing how the score was calculated  
- 🧠 Built with **normalized ratios**, so all values are scaled fairly no matter the units

> Whether you’re a min-maxer or just want to get the best results from the time you have, this report has you covered.

---

## 📦 What’s in the Repo

- `README.md` – This friendly overview  
- [`/docs`](./docs/) – Documentation for the data model, visuals, and how the DAX logic works under the hood  
  - [Measures Overview](./docs/measures_description.md) – Breakdown of the scoring logic  
  - [Visuals Walkthrough](./docs/visuals_description.md) – Explanation of what you’re looking at  
- [`/power_query`](./power_query/) – M code and query logic  
- [`/images`](./images/) – Screenshots and diagrams  
- [`dax_measures.xlsx`](./docs/dax_measures.xlsx) – Every measure used in the model  
- [`LICENSE`](./LICENSE) – Creative Commons (non-commercial, with attribution)


---

## 🧠 How the Logic Works

Each recipe has four key attributes:

| Attribute     | Meaning                                |
|--------------|----------------------------------------|
| **Profit**    | Total revenue minus cost               |
| **Cook Time** | Minutes required to prepare            |
| **Servings**  | Number of portions it produces (delays payout) |
| **XP**        | Experience gained on completion        |

You use sliders to tell the report how much each one matters to you.

The score for each recipe is calculated using a custom formula:

- The values are **normalized as ratios**, so they’re comparable  
- Each metric is raised to the **power of its selected weight**  
- Positive weights go in the **numerator**, negative ones in the **denominator**  
- This creates a scoring system that dynamically shifts based on your goals

> It’s like letting DAX play matchmaker between you and your perfect bake.

Curious about the actual math?  
→ Check out the [Measures Overview](./docs/measures_description.md) to see how it’s built.


---

## 🎯 Example Playstyles (Presets)

| Strategy     | Profit | Cook Time | Servings | XP | Description |
|--------------|--------|-----------|----------|----|-------------|
| Quick Cash   | 4      | –4        | –2       | 1  | Big money, fast, small batches  
| XP Farm      | 1      | –2        | –2       | 4  | Level up quickly, no long bakes  
| Party Host   | 1      | –2        | 4        | 0  | Feed a crowd, slow and steady  
| Balanced     | 2      | –2        | 1        | 1  | Well-rounded without extremes  

---

## 🖼️ Screenshots

| Main View | Weight Sliders | Presets |
|-----------|----------------|---------|
| ![Main View](./images/pages/ranked_recipes.png) | ![Sliders](./images/pages/sliders_and_bookmarks.png) | ![Presets](./images/pages/bookmarks.png) |

---

## 📂 How to Use

1. Open the `.pbix` file in **Power BI Desktop** (free from Microsoft)
2. Adjust the weight sliders based on what matters to you
3. Watch the recipe rankings update instantly
4. Hover over any recipe to see its breakdown

> Note: Some people from Reddit might ask “how do I open this?” — it’s a Power BI file! Just download [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).

---

---

## 🔐 License

This project is licensed under the [Creative Commons Attribution-NonCommercial 4.0 International License](./LICENSE).

You’re welcome to share it, remix it, adapt it, or use it for your own personal playstyle exploration — just don’t sell it or use it commercially without reaching out first.

> TL;DR: Go wild. Just don’t try to turn this into a bakery optimization SaaS without giving me a cut. 🧁


---

## 🤝 Why This Exists

I’ve always loved fan-made tools and mods — from Fallout 2 save editors to Factorio calculator builds. This is my version of that. I hope it’s useful, inspiring, and maybe even fun to mess with.

And if you’re the kind of person who loves digging into sliders and systems to chase optimal outcomes?  
You’ll fit right in.

---

Let me know if you use it or if you want help building your own variant. I’d love to see it evolve 🧁
