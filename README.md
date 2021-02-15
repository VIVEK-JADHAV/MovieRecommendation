# Movie Recommendation System
This project has various ways of implementing recommendation system.
The dataset used is MovieLens dataset from Kaggle. The files I have used are:
* movies_metadata.csv: It has all the information about the movie like movieId, title, genre, language, vote_average, vote_count
* link.csv: This file connects movieId with IMDBId
* ratings_small.csv: This file has ratings given by different users for different movies. It is a small portion of original file.

### Exploratory Data Analysis
EDA was performed on ratings,movieId and userId features

#### Analysing ratings feature
* Ratings range from 0.5 to 5 in the increments of 0.5
* Users have rated a large amount of movies with ratings 3 and 4

![Ratings](https://github.com/VIVEK-JADHAV/MovieRecommendation/blob/main/Images/Ratings.JPG)

#### Analysing movie feature
* Every movie has been rated by atleast one user.
* 50% of movies have been rated 27 or less number of times
* Most of the movies have fewer ratings.
* There are few movies which been rated more than 200 times.

![MovieIdDistribution](https://github.com/VIVEK-JADHAV/MovieRecommendation/blob/main/Images/Movies.JPG)

#### Analysing user feature
* Every user has rated minimum of 2 movies.
* 50% of users have rated 31 or less number of movies.
* Most of the users have rated fewer movies.
* There are users who have rated more than 200 movies.

![UserDistribution](https://github.com/VIVEK-JADHAV/MovieRecommendation/blob/main/Images/Users.JPG)

### Cold Start Problem
If a new user has not rated any movie in the past, then this model will recommend movie for such users.
Using the weighted ratings formula of IMDB, top movies in that particular genre and language is recommended.

![WeightedRating](https://github.com/VIVEK-JADHAV/MovieRecommendation/blob/main/Images/WeightedRating.JPG)

In a nutshell, this formula gives higher priority to movies which have more votes and higher rating and 
if the votes are less than threshold, it pushes towards global mean of ratings.

![ColdStartExample](https://github.com/VIVEK-JADHAV/MovieRecommendation/blob/main/Images/ColdStart.JPG)


### User-User Similarity
In this model,ratings of the user is used to find cosine similarity between a given user and all other users.
Movies of top similar users is listed out. From this list, movies not rated by the given user is recommended.

### Item-Item Similarity
In this model, cosine similarity between given movie and all other movies is computed and top similar movies are recommended.

### Matrix Factorization using SVD
The Netflix prize algorithm is used as optimization equation.

![OptimizationEquation](https://github.com/VIVEK-JADHAV/MovieRecommendation/blob/main/Images/OptimizationEquation.JPG)

![PredictedRating](https://github.com/VIVEK-JADHAV/MovieRecommendation/blob/main/Images/Prediction.JPG)

where:
* rui :Actual rating by user u on movie i
* r^ui: Predicted rating for user u on movie i
* μ : Global average of all the ratings
* bu : Bias corresponding to user u
* bi : Bias corresponding to movie i
* qi : Vector corresponding to movie i
* pu : Vector corresponding to user u
* λ : Regularization term

* Suprise library has built in implementation of this algorithm
* GridSearchCV is used to find the best hyperparameters: learning_rate, number_of_epochs and regularisation term.
* bu,bi,qi and pu are learnt through Gradient Descent algorithm.
* The cross validation gave a result of 0.9 RMSE.
* The trained model was used to predict rating of known value and the ratings were close to each other.

![PredictionExample](https://github.com/VIVEK-JADHAV/MovieRecommendation/blob/main/Images/SVDResult.JPG)


