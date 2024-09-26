# F1 Rank Prediction
For my project I decided to do F1 rank prediction. What this means is that I would predict the outcome of a race for a particular driver.
## Resources
https://www.youtube.com/watch?v=YUsx5ZNlYWc
https://www.geeksforgeeks.org/random-forest-regression-in-python/
https://www.comet.com/site/blog/random-forest-regression-in-python-using-scikit-learn/
https://www.datacamp.com/tutorial/random-forests-classifier-python
https://github.com/JaideepGuntupalli/f1-predictor/blob/trunk/model-notebooks/F1.ipynb
Credit to Ori for helping me think of a few concepts(ranking).

## Background/Context
### General Background
In Formula 1(F1), there are a lot of different variables that affect race outcome. There are 20 drivers and 10 teams on the grid(in each race). Each driver has a teammate, but they don't always work together. Each team(constructor) builds their own car, meaning that not every car is the same. Typically in F1, there are good and bad drivers and good and bad constructors. If a good driver is in a bad car, they won't do well. If a bad driver is in a good car, they will do ok. Finally, if a good driver is in a good car, they will dominate F1. 
### Qualifying
Before each race, there is another "race" of sorts. This is called qualifying. In qualifying, there are 3 sessions that order the drivers on the grid to start the race. The order is based on time: if a driver gets a better time in qualifying, they get a higher grid position. Because starting position can be so vital in many circuits, it is a HUGE factor in predicting race outcome.
### Scoring
When I talk about scoring points, I mean race position. The top 10 drivers in a race earn points, the other 10 do not. Scoring points means that a driver is consistent or at least in the top 10. These all add up to a final constructor/driver championship, which decrees the best team and best driver in the world that season/year.

## Prediction Basis
In order to predict the outcome of any race, there are 3 different metrics I will input into my model:
### 1. Driver Performance
#### Driver Reliability
When it comes to driving, reliability is incredibly important. If a driver is reliable, they have few crashes and finish in decent positions often(I.E. they don't get lapped 17 times in a race). This is incredibly important in predicting race outcome because it predicts if a driver will DNF or not, or if a driver consistently is just bad, they will stay in the lower places in prediction.
#### Driver Experience
Experience is a huge factor in driver skill. The most experienced drivers(Fernando Alonso, Lewis Hamilton) are often the most skilled drivers. Of course, there may be some young hotshot like Max Verstappen or Lando Norris, but they crash more often than Hamilton and Alonso; Hamilton and Alonso are consistent. This ties with reliability, but even in a horrible car, Alonso and Hamilton are able to squeeze all the performance out of their car possible. This allows them to be good in a bad car.
#### Driver Form
This collects data on how many points a driver has scored in the past 5 races. If they are experienced but have sudden drops in performance, this is where we can predict those drops in performance. Also, if a driver has scored 0 points in the past 5 races, we can assume they aren't going to score any more for the predicted race.
### 2. Qualifying
This is pretty simple. As mentioned earlier, qualifying is probably the largest factor in predicting race outcome. The better you qualify, the higher position you are likely to get.
### 3. Constructor Performance
Also pretty simple, this poses the question: is the car any good? We find the last 5 races and see how the entire team is performing, if they score a bunch of points, we can assume the car is good, if they score no points, we can assume the car is bad.

## Model
I decided to use a Random Forest Regressor, as my data is all over the place and a random forest regressor is a good option for a stable, not overfitted model. 
A Random Forest Regressor takes a bunch of decision trees and averages the predicted output of them all. 
It bootstraps(takes sample data, measures, then returns it) and then goes through another process called bagging: it makes a bunch of individual models(decision trees) using these samples and averages the predictions.
### Results/Accuracy
##### The model had an r^2 value of: 0.865
##### Mean Squared Error: 8.41
##### Mean Absolute Error: 1.96


## Future of Project
In the future of this project, I would likely have more input(teammate comparisons, average lap times for constructor and driver) to add consistency to the model. I would also likely create a classification model to be able to rank and input an entire race. If any more data would become available(tyre wear, driver consitency at turns, etc..) the model would become a lot more accurate as well. In general, there is a lot more data out there that I didn't have access to(private to teams), so with that data this model could be a lot more accurate.
