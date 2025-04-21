# 📊 Visuals Overview

This report includes five main pages—each focused on a specific theme—and a set of tooltip pages for interactive context. All visuals follow a consistent layout with familiar slicers, dynamic KPIs, and clean drill-through logic.

---

## Executive Summary

High-level snapshot of profitability, quality, and labor efficiency.

**Highlights:**
- Gross Profit Variance via Decomposition Tree (Dept → Machine → Part)  
- Trend line: Gross Profit per Labor Hour  
- Top Scrap Reasons (Pie Chart)  
- KPIs:  
  - Gross Profit (actual, % variance)  
  - Scrap %  
  - Pieces per Labor Hour

> Tooltips enhance scrap and variance visuals with part-level context.

---

## Plan vs. Actual

Compare planned vs. actual costs across labor, burden, and materials.

**Highlights:**
- Trend lines for Sales and GP % Variance  
- Table of job-level cost deltas  
- KPIs:  
  - GP Variance (absolute and %)  
  - Cost category breakdown (actual vs. plan)

> Hover to explore specific job contributors or drill through by part.

---

## Labor Productivity

Track how efficiently jobs convert labor into output and margin.

**Highlights:**
- Scatterplot: Cycle Time vs. GP per Hour (with quadrant lines)  
- PPLH trend over time and by machine  
- Labor table: Cycle time, labor cost, margin per piece  
- KPIs:  
  - Pieces per Labor Hour  
  - Labor Seconds per Piece  
  - GP per Piece / GP per Hour

> Zoom/slider tools help isolate machines by performance quadrant.

---

## Job Flow

Visualize production timelines, delays, and throughput patterns.

**Highlights:**
- Histogram: Jobs bucketed by duration (1–3 days, 4–7, etc.)  
- Line chart: Late Job Rate over time  
- Bar: % of Late Jobs by Machine  
- Table: Due dates, close dates, durations, status  
- KPIs:  
  - Avg Duration  
  - % Late  
  - Days Past Due (avg)

> Duration bucketing uses calculated tables, not model joins.

---

## Quality & Scrap

Dig into scrap totals and reasons across parts and departments.

**Highlights:**
- Scrap Qty by Reason and Department (bars)  
- Scrap % trend by quarter  
- Job-level scrap detail table  
- KPIs:  
  - Total Scrap  
  - Scrap %

> Scrap tooltips break down job-level causes without cluttering visuals.

---

## Tooltip Pages

Hover-driven context views built for minimal disruption.

**Included Tooltips:**
- Scrap Reason – Part-level contributors  
- Variance – Planned vs. actual per job  
- Labor – Hours, output, margin by job  
- Decomp Tree – Financial contributors by category

All tooltips are filter-aware and inherit context from the source visual.

---

## Design Notes

- Slicers appear in a consistent top-row layout across pages  
- Visual types and color mapping reinforce outcomes (e.g., red = loss)  
- KPIs use consistent formatting and spacing  
- Tooltips, decomposition, and drill-down keep insights layered—not cluttered
