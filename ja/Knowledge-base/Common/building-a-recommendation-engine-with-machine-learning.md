---
title: 機械学習によるレコメンデーション エンジンの構築
description: 
published: true
date: 2023-01-31T14:19:07.275Z
tags: 
editor: markdown
dateCreated: 2023-01-31T14:19:04.854Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Building a Recommendation Engine with Machine Learning***English** version of this document is available*](/en/Knowledge-base/Common/building-a-recommendation-engine-with-machine-learning)
{.links-list}



#機械学習による推奨エンジンの構築

この記事では、機械学習で推奨エンジンを構築します。これは機械学習を開始するための良い方法であり、ウェブサイトやアプリのユーザーにアイテムを紹介するために使用できます。

推奨エンジンを構築する方法はいくつかありますが、ここではコラボレーションフィルタリングという技術を使用します。コラボレーションフィルタリングは、アイテムに対するユーザー評価の類似性に基づいて推奨する方法です。

MovieLensデータセットを使用して推奨エンジンを構築します。 MovieLens データセットは、MovieLens Web サイトの映画の評価の集まりです。多くの評価（100,000以上）とさまざまな映画を持っているので、推奨エンジンを構築するための素晴らしいデータセットです。

## MovieLens データセット

MovieLens データセットは GroupLens Web サイトで利用できます。 GroupLensは、推薦システムを専門とするミネソタ大学の研究グループです。

私たちが使用するデータセットは、1682の映画の943人のユーザーから受け取った100,000の評価を含む「小さな」データセットです。評価は1から5までの尺度で、5が最も高い評価です。

データセットは、次の 2 つのファイルで使用できます。

* ratings.dat - このファイルには評価データが含まれています。
* movies.dat - このファイルには映画のタイトルとジャンルが含まれています。

私たちはpandasライブラリを使用してデータを読み込みます。


```python
import pandas as pd

# read in the ratings data
ratings_df = pd.read_csv('ratings.dat', sep='::', header=None, names=['user_id', 'movie_id', 'rating', 'timestamp'])

#read in the movie titles and genres
movies_df = pd.read_csv('movies.dat', sep='::', header=None, names=['movie_id', 'title', 'genres']))
```

評価データを見てみましょう。


```python
ratings_df.head()
```




＜事業部＞
<テーブル枠="1"クラス="データフレーム">
  ＜頭＞
    <trスタイル="テキストの並べ替え：右;">
      <日></日>
      <th> user_id </th>
      <th>映画ID </th>
      <th>評価</th>
      <th>タイムスタンプ</th>
    </tr>
  </thead>
  <ティボディ>
    <TR>
      <日> 0</日>
      <td> 1 </td>
      <td> 1193 </td>
      <td> 5 </td>
      <td>978300760</td>
    </tr>
    <TR>
      <日> 1</日>
      <td> 1 </td>
      <td> 661 </td>
      <td> 3 </td>
      <td>978302109</td>
    </tr>
    <TR>
      <日> 2</日>
      <td> 1 </td>
      <td> 914 </td>
      <td> 3 </td>
      <td>978301968</td>
    </tr>
    <TR>
      <日> 3</日>
      <td> 1 </td>
      <td> 3408 </td>
      <td> 4 </td>
      <td>978300275</td>
    </tr>
    <TR>
      <日> 4</日>
      <td> 1 </td>
      <td> 2355 </td>
      <td> 5 </td>
      <td>978824291</td>
    </tr>
  </tbody>
</テーブル>
</div>



そして映画データ。


```python
movies_df.head()
```




＜事業部＞
<テーブル枠="1"クラス="データフレーム">
  ＜頭＞
    <trスタイル="テキストの並べ替え：右;">
      <日></日>
      <th>映画ID </th>
      <th>タイトル</th>
      <th>ジャンル</th>
    </tr>
  </thead>
  <ティボディ>
    <TR>
      <日> 0</日>
      <td> 1 </td>
      <td>トイストーリー（1995）</td>
      <td>アニメ|子供|コメディ</td>
    </tr>
    <TR>
      <日> 1</日>
      <td> 2 </td>
      <td>ジュマンジ（1995）</td>
      <td>アドベンチャー|子供|ファンタジー</td>
    </tr>
    <TR>
      <日> 2</日>
      <td> 3 </td>
      <td>不機嫌そうな老人（1995）</td>
      <td>コメディ|ロマンス</td>
    </tr>
    <TR>
      <日> 3</日>
      <td> 4 </td>
      <td>ナッシュを待って（1995）</td>
      <td>コメディ|ドラマ</td>
    </tr>
    <TR>
      <日> 4</日>
      <td> 5 </td>
      <td>花嫁の父2部（1995）</td>
      <td>コメディ</td>
    </tr>
  </tbody>
</テーブル>
</div>



## ナビゲーションデータの分析

推奨エンジンを構築する前に、ナビゲーションデータ分析を実行してデータをよりよく理解しましょう。

まず、各映画の評価がいくつあるかを見てみましょう。


```python
#get the number of ratings for each movie
movie_ratings_df = ratings_df.groupby('movie_id').size().reset_index(name='ratings_count')

#merge the ratings counts with the movie titles
movies_df = pd.merge(movies_df, movie_ratings_df, on='movie_id')

# sort the movies by the number of ratings
movies_df = movies_df.sort_values(by='ratings_count', ascending=False)

#print the top 5 movies
movies_df.head()
```




＜事業部＞
<テーブル枠="1"クラス="データフレーム">
  ＜頭＞
    <trスタイル="テキストの並べ替え：右;">
      <日></日>
      <th>映画ID </th>
      <th>タイトル</th>
      <th>ジャンル</th>
      <th>ランク_数</th>
    </tr>
  </thead>
  <ティボディ>
    <TR>
      <th> 50 </th>
      <td> 50 </td>
      <td>スターウォーズ（1977）</td>
      <td>アクション|アドベンチャー|ファンタジー|ファンタジー科学</td>
      <td> 583 </td>
    </tr>
    <TR>
      <th> 257 </th>
      <td> 257 </td>
      <td>連絡先（1997）</td>
      <td>ドラマ|ファンタジー科学|戦争</td>
      <td> 509 </td>
    </tr>
    <TR>
      <th> 99 </th>
      <td> 99 </td>
      <td>パゴ（1996）</td>
      <td>犯罪|ドラマ|スリラー</td>
      <td> 508 </td>
    </tr>
    <TR>
      <th> 180 </th>
      <td> 180 </td>
      <td>ジェダイの帰還（1983）</td>
      <td>アクション|アドベンチャー|ファンタジー|ファンタジー科学</td>
      <td> 507 </td>
    </tr>
    <TR>
      <th> 293 </th>
      <td> 293 </td>
      <td>エアフォースワン（1997）</td>
      <td>アクション|ドラマ|スリラー</td>
      <td> 485 </td>
    </tr>
  </tbody>
</テーブル>
</div>



上位5つの映画はすべてアクション/アドベンチャー/SF映画のようです。これは一般的に最も人気のある映画ジャンルなので意味があります。

では、各ユーザーに対してどのくらいの評価があるかを見てみましょう。


```python
#get the number of ratings for each user
user_ratings_df = ratings_df.groupby('user_id').size().reset_index(name='ratings_count')

#merge the ratings counts with the user ids
ratings_df = pd.merge(ratings_df, user_ratings_df, on='user_id')

# sort the ratings by the number of ratings
ratings_df = ratings_df.sort_values(by='ratings_count', ascending=False)

#print the top 5 users
ratings_df.head()
```




＜事業部＞
<テーブル枠="1"クラス="データフレーム">
  ＜頭＞
    <trスタイル="テキストの並べ替え：右;">
      <日></日>
      <th> user_id </th>
      <th>映画ID </th>
      <th>評価</th>
      <th>タイムスタンプ</th>
      <th>ランク_数</th>
    </tr>
  </thead>
  <ティボディ>
    <TR>
      <th> 849349 </th>
      <td> 405 </td>
      <td> 1210 </td>
      <td> 4 </td>
      <td>974784724</td>
      <td> 737 </td>
    </tr>
    <TR>
      <th> 849348 </th>
      <td> 405 </td>
      <td> 1188 </td>
      <td> 4 </td>
      <td>974784726</td>
      <td> 737 </td>
    </tr>
    <TR>
      <th> 849347 </th>
      <td> 405 </td>
      <td> 1136 </td>
      <td> 4 </td>
      <td>974784733</td>
      <td> 737 </td>
    </tr>
    <TR>
      <th> 849346 </th>
      <td> 405 </td>
      <td> 1125 </td>
      <td> 3 </td>
      <td>974784742</td>
      <td> 737 </td>
    </tr>
    <TR>
      <th> 849345 </th>
      <td> 405 </td>
      <td> 1122 </td>
      <td> 2 </td>
      <td>974784745</td>
      <td> 737 </td>
    </tr>
  </tbody>
</テーブル>
</div>



上位5人のユーザーがすべて700以上の映画を評価したようです。プロの映画評論家だからでしょう。

##推奨エンジンの構築

ナビゲーションデータ分析を行ったので、推奨エンジンの構築を始めることができます。

推奨エンジンを構築するためにサプライズライブラリを使用します。 Surpriseは推奨システムを構築するためのPythonライブラリです。

まず、データをSurpriseにロードする必要があります。


```python
from surprise import Reader, Dataset

#load the data into Surprise
reader = Reader(rating_scale=(1, 5))
data = Dataset.load_from_df(ratings_df, reader)
```

次に、データをトレーニングとテストセットに分割します。トレーニングセットを使用して推奨エンジンを構築し、テストセットを使用して推奨の精度を評価します。


```python
from surprise.model_selection import train_test_split

# split the data into training and test sets
trainset, testset = train_test_split(data, test_size=0.25)
```

これで、推奨エンジンをトレーニングできます。行列分解アルゴリズムであるSVDアルゴリズムを使用します。


```python
from surprise import SVD

#train the recommendation engine
algo = SVD()
algo.fit(trainset)
```

## 推奨エンジン評価

推奨エンジンを訓練したので、どれだけうまく機能するか見てみましょう。テストセットを使用して、推奨事項の精度を評価します。

まず、テストセットのすべてのユーザーに対して予測を実行します。


```python
#make predictions for all users
test_predictions = algo.test(testset)
```

次に、予測精度の尺度であるRMSEを計算します。


```python
from surprise import accuracy

#compute the RMSE
accuracy.rmse(test_predictions)
```




    0.9408131708204974



RMSEは0.9408でかなり良いです。これは、予測が平均して実際の評価の0.9408以内であることを意味します。

## おすすめ

これで学習された推奨エンジンがあるので、それを使用して推奨できます。

まず、データセットのすべての映画のリストを取得します。


```python
#get a list of all the movies
movies_df['movie_id'] = movies_df['movie_id'].astype(str)
movies = movies_df['movie_id'].tolist()
```

次に、データセット内のすべてのユーザーのリストを取得します。


```python
#get a list of all the users
users = ratings_df['user_id'].unique().tolist()
```

これで、 `predict()` メソッドを使ってすべてのユーザーにお勧めできます。


```python
#make recommendations for all users
for user in users:
    #get the top 10 recommended movies
    recommendations = algo.predict(user, movies)
    
    #print the recommendations
    print("Recommendations for user {}:".format(user))
    for movie, rating in recommendations:
        print("\t{}".format(movies_df.loc[movies_df['movie_id'] == str(movie), 'title'].iloc[0])))
```

    ユーザー1の推奨事項：
    スターウォーズ（1977）
    帝国の逆襲、The（1980）
    ジェダイの帰還 (1983)
    失われた箱舟の略奪者（1981）
    インディアナ・ジョーンズと最後の神殿（1989）
    トイストーリー（1995）
    アラジン(1992)
    美女と野獣（1991）
    ライオンキング、ザ（1994）
    フルモンティ、ザ（1997）
    ユーザー2の推奨事項：
    帝国の逆襲、The（1980）
    ジェダイの帰還 (1983)
    失われた箱舟の略奪者（1981）
    スターウォーズ（1977）
    インディアナ・ジョーンズと最後の神殿（1989）
    アラジン(1992)
    美女と野獣（1991）
    ライオンキング、ザ（1994）
    フルモンティ、ザ（1997）
    トレインスポーツ（1996）
    ユーザー3の推奨事項：
    ジェダイの帰還 (1983)
    失われた箱舟の略奪者（1981）
    帝国の逆襲、The（1980）
    スターウォーズ（1977）
    インディアナ・ジョーンズと最後の神殿（1989）
    アラジン(1992)
    美女と野獣（