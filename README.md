<p align="center">
  <img width="300" src="https://thumbs.dreamstime.com/z/premier-league-20792019.jpg?w=576" alt="logo">
</p>

# Monte Carlo Simulation of the Premier League based on Modelling Goals Scored

## Introduction
This is a data-driven project that uses statistical analysis, machine learning techniques, and Monte-Carlo simulation to forecast Premier League match outcomes. We have then compared the season results along with the estimated probabilities of each fixture's possible results with the Bet365 probabilities. This README provides a comprehensive explanation of the project's objectives, methods, data sources, model specifics, and usage instructions.

## Project Overview

The **Premier League** is widely regarded as one of the most famous football leagues in the world, famed for its fierce competition and spectacular matches. The primary goal of this project is to develop a predictive model that uses multiple team qualities to forecast the rate parameter. This metric is used to statistically reflect both the home and away teams' goals in a given match. Furthermore, the model seeks to simulate these encounters to take into consideration the intrinsic unpredictability and uncertainty that define football matches.

## Libraries Used

The following Python libraries were used in this project:

```python
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
import statistics as stat
import seaborn as sns
import statsmodels.api as sm
import statsmodels.formula.api as smf
from scipy.stats import poisson
```

## Methodology

Our predictive model employs a multi-step approach:

1. **Data Collection and Preprocessing:**

   Historical Premier League data is compiled from a variety of sources. Match statistics such as match fixtures, results, goals, shots, corners, cards received, and Bet365 probabilities are retrieved from https://www.football-data.co.uk/. Defensive ratings for teams are derived from WhoScored (https://www.whoscored.com/) and are available in the provided 'Defending_Prem.xlsx' file.


2. **Feature Engineering:**

   Key features are engineered, including team form, shot accuracy, defensive performance, chances created, and booking points. These features offer critical insights into team dynamics.
We also check how these features affect the possibility of a team scoring goals.

<img align="center" src="https://github.com/ACM40960/project-Usman22201517/blob/main/Images/Correlation of features with home goals.png" width="600" height="450">
<img align="center" src="https://github.com/ACM40960/project-Usman22201517/blob/main/Images/Correlation of features with away goals.png" width="600" height="450">

We also check how the home and away goals scored in the Premier League are distributed, and since it's a count, we model it against the Poisson distribution.

<img align="center" src="https://github.com/ACM40960/project-Usman22201517/blob/main/Images/Home Goal Distribution.png" width="600" height="450">
<img align="center" src="https://github.com/ACM40960/project-Usman22201517/blob/main/Images/Away Goal Distribution.png" width="600" height="450">


3. **Poisson Regression:**

  Utilizing the gathered data and engineered features, a Poisson regression model is constructed. This model integrates various parameters to predict the expected goal counts for both home and away teams.

   - **Training Data:**

 The Poisson regression model is trained using historical data from the 2016–2022 seasons. Fixtures from this period are used as training data to establish the model's parameters.

```python
 poisson_model_home = sm.GLM(Y_trainH, X_train_with_intercept, family=sm.families.Poisson()).fit()
 poisson_model_away = sm.GLM(Y_trainA, X_train_with_intercept, family=sm.families.Poisson()).fit()
```

- **Prediction for 2023:**

     The trained model is then employed to predict outcomes for fixtures from the 2023 season, producing lambda values for home and away goals scored.
  
```python
 predicted_goals_home = poisson_model_home.predict(X_test_with_intercept)
 predicted_goals_away = poisson_model_away.predict(X_test_with_intercept)
```


4. **Monte Carlo Simulation:**

   Once the expected goal counts are determined, a Monte Carlo simulation is implemented. This simulation introduces randomness and captures the inherent uncertainty in football matches. It generates a range of potential match outcomes and their corresponding probabilities.
   

6. **Prediction and Evaluation:**

   The simulation results provide probabilities for different outcome scenarios (home win, draw, away win). These probabilities are compared with actual betting odds and we also compared the actual premier league table to the Monte Carlo simulated table for the 2022-23 season. We have provided the points comparison between the two as well.

   <img align="center" src="https://github.com/ACM40960/project-Usman22201517/blob/main/Images/Points Comparison.png" width="600" height="450">
   <img align="center" src="https://github.com/ACM40960/project-Usman22201517/blob/main/Images/Probabilities Comparison.png" width="600" height="450">

7. **Further Simulation for 2024 season**

   We have used the average home and away goals scored in the predicted table of 2023 season as lambda to simulate the fixtures of 2024 season and predicted the final league table. All the league tables have been provided in the **Images** folder. 


## Data Sources

- **Football-Data:** Historical Premier League data, including match fixtures, results, goals, shots, corners, and cards, is sourced from [Football-Data](https://www.football-data.co.uk/mmz4281/).

- **WhoScored:** Defensive ratings for teams are obtained from [WhoScored](https://www.whoscored.com/) and are included in the `Defending_Prem.xlsx` file.


## Conclusion

In the future, better algorithms could be used to model the goals scored. We can further enhance the model by including the derby results of previous matches and the stadium they were played in. Key information such as team tactics, player availability, and players’ form can be introduced in the model to enhance the simulation result.


## Authors

This work has been carried out by:
- **Usman Zahoor**
- **Tejaswi Singh Chauhan**


## REFERENCES
[1](https://doi.org/10.1016/j.ijforecast.2018.01.003)Rahul Baboota, Harleen Kaur(2019). Predictive analysis and modelling football results using machine learning approach for English Premier League(PDF).Journal of Forecasting, Volume 35, Issue 2, 2019

[2](https://doi.org/10.1016/j.ijforecast.2016.11.006) Georgi Boshnakov, Tarak Kharrat, Ian G. McHale (2017). A bivariate Weibull count model for forecasting association football scores(PDF). International Journal of Forecasting, Volume 33, Issue 2, 2017.

[3](https://medium.com/swlh/predicting-the-outcome-of-the-english-premier-league-by-using-monte-carlo-method-in-r-638fbc90fd37)Menyhert Kristof (2021). Predicting the Outcome of the English Premier League By Using Monte Carlo Method (in R). 




  
