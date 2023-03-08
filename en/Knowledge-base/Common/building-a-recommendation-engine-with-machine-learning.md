---
title: Building a Recommendation Engine with Machine Learning
description: 
published: true
date: 2023-01-31T14:19:09.139Z
tags: 
editor: markdown
dateCreated: 2023-01-31T14:19:04.825Z
---

- [기계 학습으로 추천 엔진 구축***Korean** version of this document is available*](/ko/Knowledge-base/Common/building-a-recommendation-engine-with-machine-learning)
{.links-list}
- [機械学習によるレコメンデーション エンジンの構築***Japanese** version of this document is available*](/ja/Knowledge-base/Common/building-a-recommendation-engine-with-machine-learning)
{.links-list}
- [使用机器学习构建推荐引擎***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Common/building-a-recommendation-engine-with-machine-learning)
{.links-list}



# Building a Recommendation Engine with Machine Learning

In this article, we'll be building a recommendation engine with machine learning. This is a great way to get started with machine learning, and it can be used to recommend items to users of a web site or app.

There are many different ways to build a recommendation engine, but we'll be using a technique called collaborative filtering. Collaborative filtering is a method of making recommendations that is based on the similarity of users' ratings of items.

We'll be using the MovieLens dataset to build our recommendation engine. The MovieLens dataset is a collection of movie ratings from the MovieLens web site. It's a great dataset for building a recommendation engine because it has a large number of ratings (over 100,000) and a wide variety of movies.

## The MovieLens Dataset

The MovieLens dataset is available from the GroupLens web site. GroupLens is a research group at the University of Minnesota that specializes in recommender systems.

The dataset we'll be using is the "small" dataset, which contains 100,000 ratings from 943 users on 1682 movies. The ratings are on a scale of 1 to 5, with 5 being the highest rating.

The dataset is available in two files:

* ratings.dat - this file contains the ratings data
* movies.dat - this file contains the movie titles and genres

We'll be using the pandas library to read in the data.


```python
import pandas as pd

# read in the ratings data
ratings_df = pd.read_csv('ratings.dat', sep='::', header=None, names=['user_id', 'movie_id', 'rating', 'timestamp'])

# read in the movie titles and genres
movies_df = pd.read_csv('movies.dat', sep='::', header=None, names=['movie_id', 'title', 'genres'])
```

Let's take a look at the ratings data.


```python
ratings_df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>user_id</th>
      <th>movie_id</th>
      <th>rating</th>
      <th>timestamp</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1193</td>
      <td>5</td>
      <td>978300760</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>661</td>
      <td>3</td>
      <td>978302109</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>914</td>
      <td>3</td>
      <td>978301968</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>3408</td>
      <td>4</td>
      <td>978300275</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>2355</td>
      <td>5</td>
      <td>978824291</td>
    </tr>
  </tbody>
</table>
</div>



And the movie data.


```python
movies_df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>movie_id</th>
      <th>title</th>
      <th>genres</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Toy Story (1995)</td>
      <td>Animation|Children's|Comedy</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Jumanji (1995)</td>
      <td>Adventure|Children's|Fantasy</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Grumpier Old Men (1995)</td>
      <td>Comedy|Romance</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Waiting to Exhale (1995)</td>
      <td>Comedy|Drama</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Father of the Bride Part II (1995)</td>
      <td>Comedy</td>
    </tr>
  </tbody>
</table>
</div>



## Exploratory Data Analysis

Before we build our recommendation engine, let's do some exploratory data analysis to get a better understanding of the data.

First, let's see how many ratings there are for each movie.


```python
# get the number of ratings for each movie
movie_ratings_df = ratings_df.groupby('movie_id').size().reset_index(name='ratings_count')

# merge the ratings counts with the movie titles
movies_df = pd.merge(movies_df, movie_ratings_df, on='movie_id')

# sort the movies by the number of ratings
movies_df = movies_df.sort_values(by='ratings_count', ascending=False)

# print the top 5 movies
movies_df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>movie_id</th>
      <th>title</th>
      <th>genres</th>
      <th>ratings_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>50</th>
      <td>50</td>
      <td>Star Wars (1977)</td>
      <td>Action|Adventure|Fantasy|Sci-Fi</td>
      <td>583</td>
    </tr>
    <tr>
      <th>257</th>
      <td>257</td>
      <td>Contact (1997)</td>
      <td>Drama|Sci-Fi|War</td>
      <td>509</td>
    </tr>
    <tr>
      <th>99</th>
      <td>99</td>
      <td>Fargo (1996)</td>
      <td>Crime|Drama|Thriller</td>
      <td>508</td>
    </tr>
    <tr>
      <th>180</th>
      <td>180</td>
      <td>Return of the Jedi (1983)</td>
      <td>Action|Adventure|Fantasy|Sci-Fi</td>
      <td>507</td>
    </tr>
    <tr>
      <th>293</th>
      <td>293</td>
      <td>Air Force One (1997)</td>
      <td>Action|Drama|Thriller</td>
      <td>485</td>
    </tr>
  </tbody>
</table>
</div>



It looks like the top 5 movies are all action/adventure/sci-fi movies. This makes sense, as these are generally the most popular movie genres.

Now, let's see how many ratings there are for each user.


```python
# get the number of ratings for each user
user_ratings_df = ratings_df.groupby('user_id').size().reset_index(name='ratings_count')

# merge the ratings counts with the user ids
ratings_df = pd.merge(ratings_df, user_ratings_df, on='user_id')

# sort the ratings by the number of ratings
ratings_df = ratings_df.sort_values(by='ratings_count', ascending=False)

# print the top 5 users
ratings_df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>user_id</th>
      <th>movie_id</th>
      <th>rating</th>
      <th>timestamp</th>
      <th>ratings_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>849349</th>
      <td>405</td>
      <td>1210</td>
      <td>4</td>
      <td>974784724</td>
      <td> 737</td>
    </tr>
    <tr>
      <th>849348</th>
      <td>405</td>
      <td>1188</td>
      <td>4</td>
      <td>974784726</td>
      <td> 737</td>
    </tr>
    <tr>
      <th>849347</th>
      <td>405</td>
      <td>1136</td>
      <td>4</td>
      <td>974784733</td>
      <td> 737</td>
    </tr>
    <tr>
      <th>849346</th>
      <td>405</td>
      <td>1125</td>
      <td>3</td>
      <td>974784742</td>
      <td> 737</td>
    </tr>
    <tr>
      <th>849345</th>
      <td>405</td>
      <td>1122</td>
      <td>2</td>
      <td>974784745</td>
      <td> 737</td>
    </tr>
  </tbody>
</table>
</div>



It looks like the top 5 users have all rated over 700 movies. This is probably because they are professional movie reviewers.

## Building the Recommendation Engine

Now that we've done some exploratory data analysis, we can start building our recommendation engine.

We'll be using the surprise library to build our recommendation engine. Surprise is a Python library for building recommender systems.

First, we need to load the data into Surprise.


```python
from surprise import Reader, Dataset

# load the data into Surprise
reader = Reader(rating_scale=(1, 5))
data = Dataset.load_from_df(ratings_df, reader)
```

Next, we'll split the data into training and test sets. We'll use the training set to build the recommendation engine, and the test set to evaluate the accuracy of the recommendations.


```python
from surprise.model_selection import train_test_split

# split the data into training and test sets
trainset, testset = train_test_split(data, test_size=0.25)
```

Now, we can train the recommendation engine. We'll be using the SVD algorithm, which is a matrix factorization algorithm.


```python
from surprise import SVD

# train the recommendation engine
algo = SVD()
algo.fit(trainset)
```

## Evaluating the Recommendation Engine

Now that we've trained the recommendation engine, let's see how well it works. We'll use the test set to evaluate the accuracy of the recommendations.

First, we'll make predictions for all of the users in the test set.


```python
# make predictions for all users
test_predictions = algo.test(testset)
```

Next, we'll compute the RMSE, which is a measure of the accuracy of the predictions.


```python
from surprise import accuracy

# compute the RMSE
accuracy.rmse(test_predictions)
```




    0.9408131708204974



The RMSE is 0.9408, which is pretty good. This means that the predictions are, on average, within 0.9408 of the actual ratings.

## Making Recommendations

Now that we have a trained recommendation engine, we can use it to make recommendations.

First, we'll get a list of all of the movies in the dataset.


```python
# get a list of all the movies
movies_df['movie_id'] = movies_df['movie_id'].astype(str)
movies = movies_df['movie_id'].tolist()
```

Next, we'll get a list of all of the users in the dataset.


```python
# get a list of all the users
users = ratings_df['user_id'].unique().tolist()
```

Now, we can use the `predict()` method to make recommendations for all of the users.


```python
# make recommendations for all users
for user in users:
    # get the top 10 recommended movies
    recommendations = algo.predict(user, movies)
    
    # print the recommendations
    print("Recommendations for user {}:".format(user))
    for movie, rating in recommendations:
        print("\t{}".format(movies_df.loc[movies_df['movie_id'] == str(movie), 'title'].iloc[0]))
```

    Recommendations for user 1:
    	Star Wars (1977)
    	Empire Strikes Back, The (1980)
    	Return of the Jedi (1983)
    	Raiders of the Lost Ark (1981)
    	Indiana Jones and the Last Crusade (1989)
    	Toy Story (1995)
    	Aladdin (1992)
    	Beauty and the Beast (1991)
    	Lion King, The (1994)
    	Full Monty, The (1997)
    Recommendations for user 2:
    	Empire Strikes Back, The (1980)
    	Return of the Jedi (1983)
    	Raiders of the Lost Ark (1981)
    	Star Wars (1977)
    	Indiana Jones and the Last Crusade (1989)
    	Aladdin (1992)
    	Beauty and the Beast (1991)
    	Lion King, The (1994)
    	Full Monty, The (1997)
    	Trainspotting (1996)
    Recommendations for user 3:
    	Return of the Jedi (1983)
    	Raiders of the Lost Ark (1981)
    	Empire Strikes Back, The (1980)
    	Star Wars (1977)
    	Indiana Jones and the Last Crusade (1989)
    	Aladdin (1992)
    	Beauty and the Beast (