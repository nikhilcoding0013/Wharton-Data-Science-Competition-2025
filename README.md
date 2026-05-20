# Wharton High School Data Science Competition — 2025 & 2026

A multi-year sports analytics project developed for the [Wharton High School Data Science Competition](https://whsdsc.wharton.upenn.edu/), applying machine learning and statistical modeling to predict game outcomes and rank teams across two different sports domains.

---

## Table of Contents

- [2025 — NCAA Women's Basketball Preditions](#2025--ncaa-womens-basketball-predictor)
- [2026 — World Hockey League Analytics](#2026--world-hockey-league-analytics)
- [Requirements](#requirements)
- [License](#license)

---

## 2025 — NCAA Women's Basketball Predictions

### Overview

Analyzed over 5,300 NCAA Women's Division I basketball games to achieve two competition objectives:

- **Task A:** Rank teams within each region based on performance
- **Task B:** Predict outcomes of hypothetical East Region matchups

### Dataset

The competition dataset contained 5,300+ historical NCAA Division I women's basketball games, including game outcomes, team identifiers, regional division information, and performance statistics such as field goals, free throws, assists, blocks, steals, turnovers, and rebounds.

### Methodology

**Custom Elo Rating System**

Each team starts with a base Elo rating of 1500. Expected win probabilities are calculated for every matchup, and ratings are updated after each game based on:

- Actual vs. expected outcomes
- Performance adjustments from advanced stats (assists, blocks, steals, turnovers, rebounds)
- Shooting efficiency (2-point, 3-point, and free throws)

Elo ratings were used for both regional team rankings (Task A) and as input features for predictive modeling (Task B).

**Game Outcome Prediction**

Multiple linear regression with polynomial features was applied. Model features include:

- Elo-derived expected win probability
- Game-specific factors: rest days, travel distance, home/away status, and opponent strength
- Adjustments for non-D1 or incomplete teams

Output: predicted win probabilities refined using a sigmoid transformation to represent values between 0 and 1.

### Results

Final Elo-based rankings were produced for each region, capturing team strength trends throughout the season. Predicted win probabilities were generated for all hypothetical East Region matchups, balancing historical performance with advanced stats to produce realistic predictions.

### Tools & Libraries

Developed in Python using Google Colab.

```
pip install pandas numpy scikit-learn matplotlib
```

### Usage

1. Clone the repository:

```bash
git clone <repository-url>
cd <repository-folder>
```

2. Run the Jupyter notebooks in Colab to preprocess data, compute Elo ratings, train models, and generate predictions.

3. To query a team's final Elo rating:

```python
from elo_module import get_team_elo
print(get_team_elo("nc_state_wolfpack"))
```

---

## 2026 — World Hockey League Analytics

### Overview

Analyzed a full season of the fictional World Hockey League (WHL) — 32 teams, 82 games each, 1,312 total games — to address three competition objectives:

- **Task A:** Generate team power rankings based on underlying performance
- **Task B:** Predict win probabilities for 16 first-round tournament matchups
- **Task C:** Quantify and visualize offensive line quality disparity across all teams

### Dataset

The WHL dataset contains line-level game data, where each game is broken down into approximately 18 rows representing matchups between home and away offensive lines (first and second) and defensive pairings (first and second). Key fields include time on ice (TOI), expected goals (xG), shots, assists, goals, and penalty minutes per line pairing.

### Methodology

**Data Cleaning & Feature Engineering**

Raw TOI was converted from seconds to minutes. An even-strength (ES) filter was applied to isolate standard play (excluding power play, penalty kill, and empty-net situations). Power play xG was scaled down using a scalar derived from the ratio of average even-strength xG rate to power play xG rate, producing an `xg_adj` field that normalizes across game situations.

**Iterative Opponent-Adjusted Strength Rating**

Team and line strength was computed in two rounds:

- *Round 0 (baseline):* Offensive strength = total adjusted xG / total TOI; defensive strength = total adjusted xG allowed / total TOI.
- *Round 1 (opponent-adjusted):* Offensive strength = total adjusted xG / Σ(TOI × opponent defensive strength); defensive strength = total adjusted xG allowed / Σ(TOI × opponent offensive strength). This adjusts each line's performance for the quality of the opponents they faced.

TOI-weighted offensive and defensive strengths were aggregated to the team level, and a composite net strength score was computed as:

```
net_strength = offensive_strength + (1 / defensive_strength)
```

Teams were ranked by net strength, with Brazil, Thailand, and Pakistan leading the 32-team standings.

**Offensive Line Disparity (Task B)**

Using the Round 0 even-strength offensive strength values, a disparity ratio was calculated per team as the product of first-line and second-line offensive strength. Teams with the highest ratios — led by Pakistan, Thailand, and Brazil — were identified as having the strongest overall offensive line depth.

**Monte Carlo Win Probability Simulation (Task C)**

Predicted win probabilities for tournament matchups were generated using a Poisson-based Monte Carlo simulation (10,000 iterations per matchup). Expected goals per game for each team were derived from net strength scores and scaled to league average scoring rates. Home and away expected goal totals were sampled from Poisson distributions and compared across all simulations to produce home win, away win, and draw probabilities.

### Results

- 32-team power rankings produced using opponent-adjusted net strength scores
- Top 10 offensive line disparity rankings identifying teams with the strongest combined first and second lines
- Win probabilities for all 16 first-round tournament matchups generated via Monte Carlo simulation

### Tools & Libraries

Developed in Python using Google Colab.

```
pip install pandas numpy matplotlib
```

### Usage

1. Clone the repository and open the notebook in Google Colab.

2. Upload the `whl_2025` dataset CSV when prompted.

3. Run cells sequentially through:
   - Data loading and cleaning
   - Even-strength filtering and xG adjustment
   - Round 0 and Round 1 strength calculations
   - Offensive disparity ranking
   - Monte Carlo win probability simulation

---

## Requirements

Python 3.9+ is required for both projects.

```
pip install pandas numpy scikit-learn matplotlib
```

---

## Competition Context

Both projects were developed as part of the [Wharton High School Data Science Competition](https://whsdsc.wharton.upenn.edu/), an annual competition challenging high school students to apply data science to real-world sports analytics problems.

| Year | Sport | Dataset | Key Methods |
|------|-------|---------|-------------|
| 2025 | NCAA Women's Basketball | 5,300+ real games | Custom Elo ratings, polynomial regression |
| 2026 | World Hockey League (fictional) | 1,312 games, line-level | Iterative opponent-adjusted xG, Monte Carlo simulation |

---

## License

This repository is released under the MIT License. Competition datasets are subject to their original terms of use.
