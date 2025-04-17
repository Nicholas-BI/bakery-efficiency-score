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
- 🎚️ **Slider controls** let you weigh Profit, Cook Time, Servings, and XP  
- 🔁 **Presets** like “Quick Cash” and “XP Farm” make it easy to start  
- 🔍 Tooltips break down exactly *why* each recipe got its score  
- 🧮 Under the hood: ratio-based normalization, exponent weighting, and real-time DAX logic

---

## 📦 What’s in the Repo

- `README.md` – This friendly overview  
- `/docs` – Notes on the data model, DAX structure, visuals, and logic  
- `/power_query` – M code and data shaping logic  
- `/images` – Screenshots and diagrams  
- `dax_measures.xlsx` – Every measure used in the model  
- `LICENSE` – Creative Commons (non-commercial, with attribution)

---

## 🧠 How the Logic Works

Each recipe has four attributes:

| Attribute | Meaning |
|----------|---------|
| **Profit** | Total revenue minus cost  
| **Cook Time** | Minutes required to prepare  
| **Servings** | Number of portions it produces (delays payout)  
| **XP** | Experience gained on completion  

You choose how important each one is using sliders. These weights are used as **exponents** (so stronger weights have stronger effects), and the score is calculated like this:

- If you like a metric → it goes in the **numerator**  
- If you dislike a metric → it goes in the **denominator**

So a high score means that recipe fits your priorities well.

Behind the scenes, all values are **normalized as ratios** so they’re comparable, no matter the scale.

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

> Note: Some people on Reddit might ask “how do I open this?” — it’s a Power BI file! Just download [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).

---

## 🔐 License

This project is shared under [Creative Commons BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/).

> Go wild with it—remix it, improve it, share it.  
> Just don’t sell it or use it for profit without talking to me first.

---

## 🤝 Why This Exists

I’ve always loved fan-made tools and mods — from Fallout save editors to Factorio calculator builds. This is my version of that. I hope it’s useful, inspiring, and maybe even fun to mess with.

And if you’re the kind of person who loves digging into sliders and systems to chase optimal outcomes?  
You’ll fit right in.

---

Let me know if you use it or if you want help building your own variant. I’d love to see it evolve 🧁
