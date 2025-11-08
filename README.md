# Weighted Weekly Chore Picker

A single-file, client-side app to randomly **draw weighted chores** up to a weekly cap, with **no repeats in a month**, and **fair assignment** between people. It stores everything in your browser (localStorage) and supports JSON import/export.

> Live demo (GitHub Pages): `https://<your-username>.github.io/weighted-weekly-chore-picker/`  
> Replace `<your-username>` with your GitHub handle.

---

## Features

- **Weighted random draw** to a **weekly weight cap**
- **No repeats** until the monthly pool is exhausted
- **Fair assignment**
  - **Two people:** optimal weekly split that also balances **month-to-date** totals
  - **3+ people:** fairness-greedy balancing by total assigned weight
- **Auto-resets monthly**, with **Undo last week** and **Finish month** controls
- **Manage chores** table (edit names, weights, tags), **local persistence**, and **JSON import/export**
- **Dark/light** auto (respects system theme)

---

## Quick Start

1. Open `index.html` in a browser (or host via GitHub Pages).
2. Set a **Weekly weight cap** (e.g., 8–12).
3. Enter **People** (e.g., `Adam, Partner`).
4. Click **Draw this week**.  
   - Use **Finish month** on the final week to clear leftovers (may exceed cap).
   - Use **Undo last week** to revert the previous draw.
5. Edit chores/weights in **Manage chores** (auto-saves).

### Host on GitHub Pages

- **Settings → Pages → Build and deployment**  
  Source: *Deploy from a branch*  
  Branch: `main` • Folder: `/ (root)`  
- Your site will be:  
  `https://<your-username>.github.io/weighted-weekly-chore-picker/`

---

## Default Chore List (this repo’s version)

- Cleaning Shared Bathroom  
- Cleaning Bedroom Bathroom  
- Cleaning Base Floor Bathroom  
- Sweeping the main level floor  
- Sweeping the second level floor  
- Mopping the main level floor  
- Mopping the second level floor  
- Metsi Nails  
- Metsi Bath  
- Inspecting the attic  
- Weeding  
- Lawn Mowing/Weed Wacking  
- Watering the plants  
- Cleaning/Organizing the Fridge  
- Dusting the main floor  
- Dusting the second floor  
- Wiping Down Windows main floor  
- Wiping Down Windows second floor  
- General Item Cleanup/Tidying Main Floor  
- General Item Cleanup/Tidying Second Floor  
- Wiping Down Walls  
- Vacuuming Stairs/Living Room  
- Vaccuuming Upstairs

> You can edit names/weights/tags in the app. Changes persist locally in your browser.

---

## How the Draw Works

- **Draw to cap:** Repeatedly pick items with probability proportional to their **weight** while the running total ≤ **weekly cap**.  
  - If all remaining items are heavier than the cap, the **lightest** item is selected so you still get something.
- **No repeats within month:** Once drawn, an item is out of the pool until the next month (or until you reset).
- **Fairness**
  - **2 people:** The app computes an *optimal* subset for Person A to target a balanced week **and** correct month-to-date imbalance.  
    (Exact partition search up to 2²² combinations per draw; if a weekly set is unusually large, it falls back to a greedy balancer.)
  - **3+ people:** Greedy assignment by descending weight to the person with the lowest month-to-date + week-to-date total.
- **Perfect equality across the month** is guaranteed when the **sum of all monthly weights is divisible by the number of people**. Otherwise the app achieves the smallest possible difference.

---

## Data & Privacy

- **Local only**: data is stored in your browser’s localStorage.
  - Keys: `choresDeck_v1_data`, `choresDeck_v1_state`
- **Export/Import JSON** from the **Manage chores** section.

---

## Tips

- Use **cap** to control how much you pull each week. Example: a 10–12 cap works well for a moderate load.
- Want to start over now? Use **Reset month**.
- If you edit weights mid-month, the next draw will **rebalance** toward equality.

---

## Development

This repo is intentionally minimal:

