# NCAA Women’s Basketball Game Predictor — 2025 Wharton High School Data Science Competition

A machine learning project that predicts NCAA Women’s Division I basketball game outcomes and ranks teams using a custom Elo rating system. Developed in Python using Google Colab as part of the 2025 Wharton High School Data Science Competition.


## Overview

This project analyzes over 5,300 NCAA Women’s Division I basketball games to achieve two competition objectives:

- **Task A:** Rank teams within each region based on performance  
- **Task B:** Predict outcomes of hypothetical East Region matchups  

The repository includes the full data science pipeline:

- Data preprocessing and cleaning  
- Feature engineering for advanced statistics  
- Implementation of a custom Elo rating system  
- Predictive modeling using polynomial regression  
- Generation of final team rankings and predicted game outcomes  


## Dataset

The dataset provided for the competition contains:

- 5,300+ historical NCAA Division I women’s basketball games  
- Game outcomes, team identifiers, and regional division information  
- Team performance statistics, including field goals, free throws, assists, blocks, steals, turnovers, and rebounds  

This data was used to compute team strengths via Elo ratings and to generate predictive models for game outcomes.


## Methodology

### 1. Custom Elo Rating System

- Each team starts with a base Elo rating of 1500  
- Expected win probabilities are calculated for every matchup  
- Elo ratings are updated after each game based on:

  - Actual vs. expected outcomes  
  - Performance adjustments from advanced stats such as assists, blocks, steals, turnovers, and rebounds  
  - Shooting efficiency (2-point, 3-point, and free throws)  

- Elo ratings were used for:

  - Ranking teams within each region (Task A)  
  - Input features for predictive modeling (Task B)

### 2. Game Outcome Prediction

- Multiple linear regression with polynomial features was applied  
- Model features include:

  - Elo-derived expected win probability  
  - Game-specific factors: rest days, travel distance, home/away status, and opponent strength  
  - Adjustments for non-D1 or incomplete teams  

- Output: predicted win probabilities for each matchup, refined using a sigmoid transformation to represent probabilities between 0 and 1  


## Results

- **Team Rankings:**  
  Final Elo-based rankings were produced for each region, capturing team strength trends throughout the season.  

- **Win Probability Predictions:**  
  Predicted win probabilities were generated for all hypothetical East Region matchups.  

- The models successfully balanced historical performance and advanced stats to produce realistic predictions for competition evaluation.  


## Requirements

- Python 3.9+  
- Key libraries:

```bash
pip install pandas numpy scikit-learn matplotlib
```

# Basketball Game Predictor — Usage & Skills

This project was developed and executed in **Google Colab**.

## Usage

1. **Clone the repository:**

```bash
git clone <repository-url>
cd <repository-folder>
```
2. Run the provided Jupyter notebooks in Colab to:
- Preprocess and clean the dataset
- Compute Elo ratings
- Train and evaluate predictive models
- Generate predicted win probabilities

3. For querying a team’s final Elo rating:
```bash
from elo_module import get_team_elo
print(get_team_elo("nc_state_wolfpack"))
```

## Skills Demonstrated
- Machine learning and predictive modeling
- Advanced feature engineering and data preprocessing
- Custom Elo rating system implementation
- Sports analytics and probability modeling
- Data analysis with pandas and NumPy
- Model development with scikit-learn
- Collaborative data science project development

## Competition Context

Developed as part of the 2025 Wharton High School Data Science Competition, focused on NCAA Women’s Division I basketball analytics.

## License

This repository is released under the MIT License.
Competition datasets are subject to their original terms of use.
