## FIFA 2018 Challenge

**Aim for the challenge is to predict FIFA World Cup 2018 winner.**

### Getting Data --> 

To predict any situation we need backing data and data for this challenge was taken from Kaggle.com where FIFA ranking, fixtures and most importantly results are captured till date.
The results data is covers years from 1872 world cup till now.
The data is easy enough to understand. There are only 9 variables, with self-explanatory names: date, home_team, away_team, home_score, away_score, tournament, city, country, neutral (whether the match was played on neutral ground, or at the home team’s stadium).

### Preparing data --> 

Historical data is on the number fo goals scored by each team in the past.

It has been observed that the home team scores more goals than the away team since they have an field advantage over others, so for this added a goal difference between home team and away team and determine the winner.

Results data is then sliced in the process and data is considered from 1930 world cup till 2018.

### For 2018 World Cup results -->
For 2018 FIFA world cup, taken a subset of teams in dataframe to only keep the 32 teams which are qualified for 2018 World Cup.

List of Teams - 
Australia, Iran, Japan, Korea Republic, Saudi Arabia, Egypt, Morocco, Nigeria, Senegal, Tunisia, Costa Rica, Mexico, 
Panama, Argentina, Brazil, Colombia, Peru, Uruguay, Belgium, Croatia, Denmark, England, France, Germany, Iceland, Poland, Portugal, Russia, Serbia, Spain, Sweden, Switzerland
            
### Computing the results --> 
Using Logistic Regression model where given a set of data points , it attempts to predict an outcome (a win or a loss).

Also added a prediction label where the winning_team column will show "2" if the home team has won, "1" if it was a tie, and "0" if the away team has won.

### For Predictions, applying prediction model to the dataset -->

Giving a set of data to the prediction model to predict win or loss.

Model predicted  draw between Spain and Portugal but also given Spain a high probability of winning. 

In iterations, we have given set of teams to the model to predict quarters, semi finals and finals.

The model predicted a quarter final between: Uruguay vs Spain, France vs Argentina, Brazil vs Mexico and England vs Senegal

The semis Spain vs Argentina and Brazil vs England and finals between Brazil vs Argentina.

According to prediction Brazil is going to be World Champions for 2018!

## Conclusion 

There could be many ways to predict the game. Only time will tell if this model gave the correct predictions :smile:

Complete code is given in separate file 

Prediction model taken from (https://blog.goodaudience.com/predicting-fifa-world-cup-2018-using-machine-learning-dc07ad8dd576)
GitHub link : (https://github.com/itsmuriuki/FIFA-2018-World-cup-predictions)
    
