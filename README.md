# MLB Front Office Analytics Suite

A Shiny dashboard that consolidates roster construction, prospect/player valuation, and hitter metrics comparison into a single front-office tool. Built around a "Moneyball"-style extension decision framework: use scouting grades, projected performance, and market value to decide whether a pre-arbitration player is worth locking up early.

## Live App

[![Launch App](https://img.shields.io/badge/Shiny-Launch%20App-blue?style=for-the-badge&logo=rstudio)](https://ajjablonski.shinyapps.io/mlb-front-office/)

An interactive R Shiny dashboard for MLB roster and player analysis.
**[Click here to open the app](https://ajjablonski.shinyapps.io/mlb-front-office/)**. It runs in your browser with nothing to install.

## Overview

The app has three tabs, each addressing a different front-office question:

### 1. Roster Needs Analysis
Pulls a team's current 40-man roster live via the MLB Stats API (through `baseballr`) and compares actual position-group counts against an ideal roster allocation (e.g., 18 pitchers, 2 at each position player slot). Surfaces:
- A bar chart of surplus/deficit by position group
- A table of specific shortages
- The full 40-man roster breakdown

### 2. 5-Tool Player Targeter
Side-by-side comparison of any two players (MLB or MiLB) on the 20–80 scouting scale (Hit / Power / Run / Arm / Field), plus:
- A radar chart overlay of both players' tool grades
- Net surplus value for each player (market value minus current salary)
- A full financial/valuation matrix (WAR, salary, surplus value, contract status)
- A "Top 10 Closest Matches" table that finds the most statistically similar players to Player A using Euclidean distance across the five scouting tools

### 3. Hitter Metrics Comparison
Interactive scatter plot comparing current-season stats vs. projections across any two of ~19 metrics (BB%, K%, ISO, wOBA, xwOBA, wRC+, Barrel%, HardHit%, etc.), with:
- MLB vs. MiLB color coding
- An overall linear trend line
- Ability to search and highlight up to two specific players on the plot

## Background

This tool was built to explore contract-extension timing for pre-arbitration players — comparing unproven players like Samuel Basallo, Lazaro Montes, and Jesus Made against comparable historical extensions (e.g., Fernando Tatis Jr.'s pre-arb deal) to inform a sign/don't-sign decision framework based on scouting grades, statistical comparables, and surplus value.

## Requirements

**R packages:**
```r
install.packages(c(
  "shiny", "shinydashboard", "dplyr", "ggplot2",
  "fmsb", "DT", "plotly", "readxl", "tibble"
))

# baseballr is used for live MLB Stats API roster pulls
install.packages("baseballr")
```

**Data files** — the app expects three Excel files in `~/MSDS/`:

| File | Used by | Description |
|---|---|---|
| `current_stats.xlsx` | Hitter Metrics tab | Current-season hitter stats |
| `ByTheMetrics.xlsx` | Hitter Metrics tab | Projected hitter stats (e.g., FanGraphs projections) |
| `Valuable_Data.xlsx` | Player Targeter tab | Scouting grades, salary, and surplus value data |

The app will still launch if a file is missing — the affected tab will show a clear message rather than crashing.

## Running the app

```r
# From the project directory, with the three data files in ~/MSDS/
shiny::runApp("front_office_app.R")
```

## Data sources

- [FanGraphs](https://www.fangraphs.com/)
- [Baseball Savant](https://baseballsavant.mlb.com/)
- [MLB.com Prospects](https://www.mlb.com/milb/prospects)
- [Spotrac](https://www.spotrac.com/)
- [Rosternomics](https://rosternomics.com/)
- MLB Stats API (via `baseballr`)

## Author

Anthony Jablonski — Northwestern University, MSA '26 (Sports Analytics)
