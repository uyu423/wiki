---
title: 使用机器学习构建推荐引擎
description: 
published: true
date: 2023-01-31T14:19:07.254Z
tags: 
editor: markdown
dateCreated: 2023-01-31T14:19:04.853Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Building a Recommendation Engine with Machine Learning***English** version of this document is available*](/en/Knowledge-base/Common/building-a-recommendation-engine-with-machine-learning)
{.links-list}



# 使用机器学习构建推荐引擎

在本文中，我们将构建一个带有机器学习的推荐引擎。这是开始使用机器学习的好方法，它可用于向网站或应用程序的用户推荐项目。

构建推荐引擎的方法有很多种，但我们将使用一种称为协同过滤的技术。协同过滤是一种基于用户对项目评分的相似性进行推荐的方法。

我们将使用 MovieLens 数据集来构建我们的推荐引擎。 MovieLens 数据集是来自 MovieLens 网站的电影评级集合。这是构建推荐引擎的绝佳数据集，因为它具有大量评级（超过 100,000）和种类繁多的电影。

## MovieLens 数据集

MovieLens 数据集可从 GroupLens 网站获得。 GroupLens 是明尼苏达大学的一个研究小组，专门研究推荐系统。

我们将使用的数据集是“小型”数据集，其中包含 943 位用户对 1682 部电影的 100,000 条评分。评分范围为 1 到 5，其中 5 为最高评分。

数据集有两个文件：

* ratings.dat - 此文件包含评级数据
* movies.dat - 此文件包含电影标题和类型

我们将使用 pandas 库来读取数据。


```python
import pandas as pd

# read in the ratings data
ratings_df = pd.read_csv('ratings.dat', sep='::', header=None, names=['user_id', 'movie_id', 'rating', 'timestamp'])

# read in the movie titles and genres
movies_df = pd.read_csv('movies.dat', sep='::', header=None, names=['movie_id', 'title', 'genres'])
```

我们来看看评分数据。


```python
ratings_df.head()
```




<分区>
<表边框=“1”类=“数据框”>
  <头>
    <tr style="text-align: right;">
      <日></日>
      <th>user_id</th>
      <th>movie_id</th>
      <th>评分</th>
      <th>时间戳</th>
    </tr>
  </thead>
  <正文>
    <tr>
      <日>0</日>
      <td>1</td>
      <td>1193</td>
      <td>5</td>
      <td>978300760</td>
    </tr>
    <tr>
      <日>1</日>
      <td>1</td>
      <td>661</td>
      <td>3</td>
      <td>978302109</td>
    </tr>
    <tr>
      <日>2</日>
      <td>1</td>
      <td>914</td>
      <td>3</td>
      <td>978301968</td>
    </tr>
    <tr>
      <日>3</日>
      <td>1</td>
      <td>3408</td>
      <td>4</td>
      <td>978300275</td>
    </tr>
    <tr>
      <日>4</日>
      <td>1</td>
      <td>2355</td>
      <td>5</td>
      <td>978824291</td>
    </tr>
  </tbody>
</表>
</div>



还有电影数据。


```python
movies_df.head()
```




<分区>
<表边框=“1”类=“数据框”>
  <头>
    <tr style="text-align: right;">
      <日></日>
      <th>movie_id</th>
      <th>标题</th>
      <th>流派</th>
    </tr>
  </thead>
  <正文>
    <tr>
      <日>0</日>
      <td>1</td>
      <td>玩具总动员 (1995)</td>
      <td>动画|少儿|喜剧</td>
    </tr>
    <tr>
      <日>1</日>
      <td>2</td>
      <td>勇敢者游戏 (1995)</td>
      <td>冒险|儿童|奇幻</td>
    </tr>
    <tr>
      <日>2</日>
      <td>3</td>
      <td>脾气暴躁的老人 (1995)</td>
      <td>喜剧|爱情</td>
    </tr>
    <tr>
      <日>3</日>
      <td>4</td>
      <td>等待呼气 (1995)</td>
      <td>喜剧|剧情</td>
    </tr>
    <tr>
      <日>4</日>
      <td>5</td>
      <td>新娘之父下部 (1995)</td>
      <td>喜剧</td>
    </tr>
  </tbody>
</表>
</div>



## 探索性数据分析

在构建推荐引擎之前，让我们进行一些探索性数据分析以更好地了解数据。

首先，让我们看看每部电影有多少评分。


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




<分区>
<表边框=“1”类=“数据框”>
  <头>
    <tr style="text-align: right;">
      <日></日>
      <th>movie_id</th>
      <th>标题</th>
      <th>流派</th>
      <th>ratings_count</th>
    </tr>
  </thead>
  <正文>
    <tr>
      <日>50</日>
      <td>50</td>
      <td>星球大战 (1977)</td>
      <td>动作|冒险|奇幻|科幻</td>
      <td>583</td>
    </tr>
    <tr>
      <日>257</日>
      <td>257</td>
      <td>接触 (1997)</td>
      <td>剧情|科幻|战争</td>
      <td>509</td>
    </tr>
    <tr>
      <日>99</日>
      <td>99</td>
      <td>冰血暴 (1996)</td>
      <td>犯罪|剧情|惊悚</td>
      <td>508</td>
    </tr>
    <tr>
      <日>180</日>
      <td>180</td>
      <td>绝地归来 (1983)</td>
      <td>动作|冒险|奇幻|科幻</td>
      <td>507</td>
    </tr>
    <tr>
      <日>293</日>
      <td>293</td>
      <td>空军一号 (1997)</td>
      <td>动作|剧情|惊悚</td>
      <td>485</td>
    </tr>
  </tbody>
</表>
</div>



看起来前 5 名的电影都是动作/冒险/科幻电影。这是有道理的，因为这些通常是最受欢迎的电影类型。

现在，让我们看看每个用户有多少评分。


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




<分区>
<表边框=“1”类=“数据框”>
  <头>
    <tr style="text-align: right;">
      <日></日>
      <th>user_id</th>
      <th>movie_id</th>
      <th>评分</th>
      <th>时间戳</th>
      <th>ratings_count</th>
    </tr>
  </thead>
  <正文>
    <tr>
      <日>849349</日>
      <td>405</td>
      <td>1210</td>
      <td>4</td>
      <td>974784724</td>
      <td>737</td>
    </tr>
    <tr>
      <日>849348</日>
      <td>405</td>
      <td>1188</td>
      <td>4</td>
      <td>974784726</td>
      <td>737</td>
    </tr>
    <tr>
      <日>849347</日>
      <td>405</td>
      <td>1136</td>
      <td>4</td>
      <td>974784733</td>
      <td>737</td>
    </tr>
    <tr>
      <日>849346</日>
      <td>405</td>
      <td>1125</td>
      <td>3</td>
      <td>974784742</td>
      <td>737</td>
    </tr>
    <tr>
      <日>849345</日>
      <td>405</td>
      <td>1122</td>
      <td>2</td>
      <td>974784745</td>
      <td>737</td>
    </tr>
  </tbody>
</表>
</div>



看起来排名前 5 位的用户都对 700 多部电影进行了评分。这可能是因为他们是专业的影评人。

## 构建推荐引擎

现在我们已经完成了一些探索性数据分析，我们可以开始构建我们的推荐引擎。

我们将使用 surprise 库来构建我们的推荐引擎。 Surprise 是一个用于构建推荐系统的 Python 库。

首先，我们需要将数据加载到 Surprise 中。


```python
from surprise import Reader, Dataset

# load the data into Surprise
reader = Reader(rating_scale=(1, 5))
data = Dataset.load_from_df(ratings_df, reader)
```

接下来，我们将把数据分成训练集和测试集。我们将使用训练集来构建推荐引擎，使用测试集来评估推荐的准确性。


```python
from surprise.model_selection import train_test_split

# split the data into training and test sets
trainset, testset = train_test_split(data, test_size=0.25)
```

现在，我们可以训练推荐引擎了。我们将使用 SVD 算法，这是一种矩阵分解算法。


```python
from surprise import SVD

# train the recommendation engine
algo = SVD()
algo.fit(trainset)
```

## 评估推荐引擎

现在我们已经训练了推荐引擎，让我们看看它的效果如何。我们将使用测试集来评估推荐的准确性。

首先，我们将对测试集中的所有用户进行预测。


```python
# make predictions for all users
test_predictions = algo.test(testset)
```

接下来，我们将计算 RMSE，它是预测准确性的度量。


```python
from surprise import accuracy

# compute the RMSE
accuracy.rmse(test_predictions)
```




    0.9408131708204974



RMSE 为 0.9408，非常好。这意味着预测平均在实际评分的 0.9408 以内。

## 提出建议

现在我们有了一个训练有素的推荐引擎，我们可以用它来进行推荐。

首先，我们将获得数据集中所有电影的列表。


```python
# get a list of all the movies
movies_df['movie_id'] = movies_df['movie_id'].astype(str)
movies = movies_df['movie_id'].tolist()
```

接下来，我们将获得数据集中所有用户的列表。


```python
# get a list of all the users
users = ratings_df['user_id'].unique().tolist()
```

现在，我们可以使用 `predict()` 方法为所有用户提供推荐。


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

    给用户 1 的建议：
    星球大战 (1977)
    帝国反击战 (1980)
    绝地归来 (1983)
    夺宝奇兵 (1981)
    夺宝奇兵与最后的圣战 (1989)
    玩具总动员 (1995)
    阿拉丁 (1992)
    美女与野兽 (1991)
    狮子王 (1994)
    全月 (1997)
    给用户 2 的建议：
    帝国反击战 (1980)
    绝地归来 (1983)
    夺宝奇兵 (1981)
    星球大战 (1977)
    夺宝奇兵与最后的圣战 (1989)
    阿拉丁 (1992)
    美女与野兽 (1991)
    狮子王 (1994)
    全月 (1997)
    猜火车 (1996)
    给用户 3 的建议：
    绝地归来 (1983)
    夺宝奇兵 (1981)
    帝国反击战 (1980)
    星球大战 (1977)
    夺宝奇兵与最后的圣战 (1989)
    阿拉丁 (1992)
    美女和野兽 （