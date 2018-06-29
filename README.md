# crystalgazer
FIFA 2018 Challenge

Aim for the challenge is to predict FIFA World Cup 2018 winner.

Getting Data --> To predict any situation we need backing data and data for this challenge was taken from Kaggle.com where FIFA ranking, fixtures and most importantly results are captured till date.
The results data is covers years from 1872 world cup till now.
The data is easy enough to understand. There are only 9 variables, with self-explanatory names: date, home_team, away_team, home_score, away_score, tournament, city, country, neutral (whether the match was played on neutral ground, or at the home team’s stadium).

Preparing data --> 
Historical data is on the number fo goals scored by each team in the past.
results=pd.read_csv('FIFA-2018-World-cup-predictions-master/datasets/results.csv')

It has been observed that he home team scores more goals than the away team since they have an field advantage over others, so for this added a goal difference between home team and away team and determine the winner.
winner = []
for i in range (len(results['home_team'])):
    if results ['home_score'][i] > results['away_score'][i]:
        winner.append(results['home_team'][i])
    elif results['home_score'][i] < results ['away_score'][i]:
        winner.append(results['away_team'][i])
    else:
        winner.append('Draw')
results['winning_team'] = winner

#adding goal difference column
results['goal_difference'] = np.absolute(results['home_score'] - results['away_score'])
Results data has been sliced in the process and data is considered from 1930 world cup till 2018.

For 2018 World Cup results -->
For 2018 FIFA world cup, taken a subset of teams in dataframe to only keep the 32 teams which are qualified for 2018 World Cup.

worldcup_teams = ['Australia', ' Iran', 'Japan', 'Korea Republic', 
            'Saudi Arabia', 'Egypt', 'Morocco', 'Nigeria', 
            'Senegal', 'Tunisia', 'Costa Rica', 'Mexico', 
            'Panama', 'Argentina', 'Brazil', 'Colombia', 
            'Peru', 'Uruguay', 'Belgium', 'Croatia', 
            'Denmark', 'England', 'France', 'Germany', 
            'Iceland', 'Poland', 'Portugal', 'Russia', 
            'Serbia', 'Spain', 'Sweden', 'Switzerland']
            
Subsetting results data further to get results from year 1930 and onwards.
year = []
for row in df_teams['date']:
    year.append(int(row[:4]))
df_teams['match_year'] = year
df_teams_1930 = df_teams[df_teams.match_year >= 1930]


Computing the results --> 
Using Logistic Regression model where given a set of data points , it attempts to predict an outcome (a win or a loss).

logreg = LogisticRegression()
logreg.fit(X_train, y_train)
score = logreg.score(X_train, y_train)
score2 = logreg.score(X_test, y_test)

print("Training set accuracy: ", '%.3f'%(score))
print("Test set accuracy: ", '%.3f'%(score2))

Adding a prediction label where the winning_team column will show "2" if the home team has won, "1" if it was a tie, and "0" if the away team has won.

df_teams_1930 = df_teams_1930.reset_index(drop=True)
df_teams_1930.loc[df_teams_1930.winning_team == df_teams_1930.home_team,'winning_team']=2
df_teams_1930.loc[df_teams_1930.winning_team == 'Draw', 'winning_team']=1
df_teams_1930.loc[df_teams_1930.winning_team == df_teams_1930.away_team, 'winning_team']=0

For Predictions, applying prediction model to the dataset -->

predictions = logreg.predict(pred_set)
for i in range(fixtures.shape[0]):
    print(backup_pred_set.iloc[i, 1] + " and " + backup_pred_set.iloc[i, 0])
    if predictions[i] == 2:
        print("Winner: " + backup_pred_set.iloc[i, 1])
    elif predictions[i] == 1:
        print("Draw")
    elif predictions[i] == 0:
        print("Winner: " + backup_pred_set.iloc[i, 0])
    print('Probability of ' + backup_pred_set.iloc[i, 1] + ' winning: ', '%.3f'%(logreg.predict_proba(pred_set)[i][2]))
    print('Probability of Draw: ', '%.3f'%(logreg.predict_proba(pred_set)[i][1]))
    print('Probability of ' + backup_pred_set.iloc[i, 0] + ' winning: ', '%.3f'%(logreg.predict_proba(pred_set)[i][0]))

Model predicted  draw between Spain and Portuga also given Spain a high probability of winning. 

Feeding our model with set of 16 qualified teams -
group_tab = [('Uruguay', 'Russia'),
            ('Spain', 'Portugal'),
            ('France', 'Denmark'),
            ('Croatia', 'Argentina'),
            ('Brazil', 'Switzerland'),
			('Sweden', 'Mexico'),
            ('England', 'Belgium'),
            ('Japan', 'Senegal')]
            
    
