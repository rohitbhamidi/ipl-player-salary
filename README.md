# DataScienceCap2

# **Problem Statement**
The Indian Premier League (IPL) has become a global cricket phenomenon since its inception in 2008, driving growth in player salaries. This project will develop a Machine Learning model to predict the player salary based on statistical aggregate features. In doing so, I will develop a framework for the IPL franchises to make more informed decisions during player auctions on the expected salary of the players.

# **Approach**
The data for this project was sourced from two distinct repositories. Firstly, ball-by-ball match data spanning the years 2008 to 2021 was acquired from the dataset hosted on Kaggle (https://www.kaggle.com/datasets/vora1011/ipl-2008-to-2021-all-match-dataset). Secondly, salary information of players was extracted from the online resource available at http://www.cricmetric.com/ipl/salary/. 

## **1. Data Wrangling and Feature Engineering**
During the data wrangling and feature engineering phase, the match data was integrated and filtered, consolidating it with relevant attributes such as player salaries and roles. The ball-by-ball data was used to calculate batting and bowling statistics for players across multiple seasons.
For batters, the following features were engineered:
1. **balls_faced**: Total number of balls faced by the batter.
2. **total_runs**: Cumulative runs scored by the batter.
3. **batting_avg**: Batting average calculated as the ratio of total runs to the number of wicket deliveries faced.
4. **strike_rate**: Strike rate calculated as the percentage of runs scored per ball faced.
5. **50s**: Number of half-centuries (scores between 50 and 99) achieved by the batter.
6. **100s**: Number of centuries (scores of 100 or more) achieved by the batter.
7. **4s**: Total number of boundaries (4 runs) hit by the batter.
8. **6s**: Total number of sixes (6 runs) hit by the batter.

For bowlers, the following features were engineered:
1. **balls_bowled**: Total number of balls bowled by the player.
2. **total_runs**: Cumulative runs conceded by the bowler.
3. **total_wickets**: Total number of wickets taken by the bowler.
4. **bowling_avg**: Bowling average calculated as the ratio of total runs conceded to the total wickets taken.
5. **economy**: Bowling economy rate calculated as runs conceded per over bowled.
6. **strike_rate**: Bowling strike rate calculated as the ratio of balls bowled to wickets taken.
7. **3whs**: Number of matches where the bowler took between 3 and 4 wickets.
8. **5whs**: Number of matches where the bowler took 5 or more wickets.
9. **dots**: Total number of dot deliveries (no runs scored) bowled by the player.
10. **4s**: Total number of boundaries (4 runs) conceded by the bowler.
11. **6s**: Total number of sixes (6 runs) conceded by the bowler.

## **2. EDA**
The target variable for the analysis was the next-year salary for each player. The initial hypothesis was that the biggest determining factor of a player's next-year salary was the player's current salary. The following graphs corroborated that hypothesis:
<div style="display: flex; flex-direction: row;">
  <img alt="Plot of Current vs Next-Year Salary: Batters" src="./images/cy-ny-salary-batters.png" width="45%">
  <img alt="Plot of Current vs Next-Year Salary: Bowlers" src="./images/cy-ny-salary-bowlers.png" width="45%">
</div>

Furthermore, after principal component analysis, it was determined that the problem of predicting player salary is almost one-dimensional. If required, we could expand our analysis to 4 dimensions for batting or bowling. Similar arguments could be made for including more features, but ultimately, that would be decided during the evaluation of model performance.
<div style="display: flex; flex-direction: row;">
  <img alt="Principal Component Plot: Batters" src="./images/pca-batting.png" width="45%">
  <img alt="Principal Component Plot: Bowlers" src="./images/pca-bowling.png" width="45%">
</div>

## **3. Model Selection**
The metric chosen to evaluate the various regression models was Mean Absolute Error (MAE). This is due to several reasons:
* The absolute difference between the predicted and actual salary has a real-world interpretation. MAE directly measures the average salary prediction error, which aligns with estimating player salaries accurately.
* MAE is less sensitive to outliers compared to other metrics because it treats all errors equally without squaring them. This makes it a good choice since outliers can disproportionately affect the model's performance evaluation.
* MAE is a linear metric, meaning that errors are considered proportionally. 

The following two graphs show the performance of several tested models against number of selected features.
<div style="display: flex; flex-direction: row;">
  <img alt="MAE vs k Selected Features: Batters" src="./images/model-selection-batting.png" width="45%">
  <img alt="MAE vs k Selected Features: Bowlers" src="./images/model-selection-bowling.png" width="45%">
</div>

In both cases, it was determined that the best-performing models were Support Vector Regression with $k=4$ selected features. This suggests that the relationship between the predictor variables (features) and the target variable (next-year salary) is not purely linear. The model's robustness to outliers and handling of complex relationships imply that the dataset might contain varying levels of influence from different features. As more data becomes available, it might be useful to limit the number of selected features below 4 in order to balance model performance against computing resources.

The batting SVR model was fine-tuned, and found the following optimal hyperparameters: 'C' (Regularization parameter) set to 10, 'epsilon' (Epsilon parameter for margin of error) set to 0.01, and the 'kernel' chosen as 'linear'. This parameter configuration yielded an R^2 score of 0.691, and an MAE score of 0.252.

The bowling SVR model was fine-tuned, and found the following optimal hyperparameters: 'C' (Regularization parameter) set to 1, 'epsilon' (Epsilon parameter for margin of error) set to 0.01, and the 'kernel' chosen as 'linear'. This parameter configuration yielded an R^2 score of 0.653, and an MAE score of 0.265.

## **4. Predictions and Uses**
A function, **`predict_salary`** was developed to leverage the trained SVR models to make predictions. The input data is inputted in the form of the original data with the engineered features (listed above). Due to the nature of the generally-available statistics in cricket, the engineered features are easily accessible for any player in the IPL.

*Possible use cases*:
* Player Valuation and Auction Strategy: By accurately estimating a player's potential next-year salary, franchises can make more informed decisions when bidding for players.
* Talent Scouting and Recruitment: Talent scouts can leverage the insights from this project to identify promising players with the potential for high future salaries.
* Player Performance Analysis and Contract Negotiation: Cricket players and their agents can leverage the model during contract negotiations. By understanding the key performance metrics that contribute to higher salaries, players can focus on improving specific aspects of their game. Agents can use the predictive model to provide evidence-based salary expectations.

# **Further Questions**
