# DataScienceCap2

# Problem Statement
The Indian Premier League (IPL) has become a global cricket phenomenon since its inception in 2008, driving growth in player salaries. This project will develop a Machine Learning model to predict the player salary based on statistical aggregate features. In doing so, I will develop a framework for the IPL franchises to make more informed decisions during player auctions on the expected salary of the players.

# Approach
The data for this project was sourced from two distinct repositories. Firstly, ball-by-ball match data spanning the years 2008 to 2021 was acquired from the dataset hosted on Kaggle (https://www.kaggle.com/datasets/vora1011/ipl-2008-to-2021-all-match-dataset). Secondly, salary information of players was extracted from the online resource available at http://www.cricmetric.com/ipl/salary/. 

## 1. Data Wrangling and Feature Engineering
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

The player-match interaction was investigated, leading to the creation of merged datasets capturing detailed batting and bowling features.

## 2. EDA

## 3. Preprocessing and Training

## 4. Model Selection

## 5. Predictions

# Further Questions
