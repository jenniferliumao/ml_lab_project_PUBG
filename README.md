# PUBG Finish Placement Prediction
MSDS699 final project   
Group Member: Peng Liu, Xuxu Pan, Min Che

### What is PUBG? 🦄
It’s short for PlayerUknown’s BattleGrounds, a very popular battle royale-style video game. In this game, you are dropped onto an island without anything in hand, but with 99 other players most of whom are your enemies. You have to explore and fight other players until only one is left standing. Meanwhile, the playzone continues to shrink until the last minute of the game. 

# Project Goal
The goal of this project is to predict the finish placement of the PlayerUknown’s BattleGrounds(PUBG) players.

# Outlines
- Data Description
- Data Processing
- Modeling
- Summary
- Takeaways
- Future works

# Data Description
- Data source: https://www.kaggle.com/c/pubg-finish-placement-prediction/data  
- Target：winPlacePerc, player’s percentile in one game (float, 0 to 1).  
- Number of observations: >4 M, each row contains a player's post-game stats.
- Number of raw features: 28, including player’s stats such as assists, boosts, damage, kills, player per match, player per group, walk distance...

# Data Processing
We added 2 new features: player per match and player per group. To eliminate possible outliers, we dropped matches that have less than 80 players or have group with more than 4 players. We also down sample the data to 165 thousand rows and dropped 4 highly related features. Finally, we made a train-validation-test split.

# Modeling
We fitted 3 models: linear regression without tuning as our baseline, decision tree and random forest, with hyperparameters tuned by RandomizedSearchCV. We choose Median absolute error as our north star metrics because it is more robust to outliers than RMSE.

# Summary
Random forest model has the lowest MEDAE (around 0.036) on the validation set. So, we decided to choose random forest model as our final model. The tuned random forest model selected about 10 important features out of 24. Top three important features include killPlace, which is the ranking of number of enemies killed by the player in a match, walkDistance, which is how far the player walked in a match and kills, which is the number of enemies killed by the player. Seems that some of the important features are highly correlate with each other.

# Takeaways
- Technical key takeaways:
  - Random forest improves generality.
  - Feature engineering matters.

- Non-technical key takeaways:
  - The best killer wins!
  - Walk around and explore more.
  - Collect sufficient boosters boost yourself promptly.
  - Kill from afar.

# Future Works
- Can we cluster players based on their strategies and behaviors?
  - i.e. killer or hide-and-seeker?
- If we label players by clustering, does it help to improve the regressor?
