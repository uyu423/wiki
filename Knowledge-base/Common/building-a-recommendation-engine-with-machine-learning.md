---
title: 기계 학습으로 추천 엔진 구축
description: 
published: true
date: 2023-01-31T14:19:07.227Z
tags: 
editor: markdown
dateCreated: 2023-01-31T14:19:04.827Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Building a Recommendation Engine with Machine Learning***English** version of this document is available*](/en/Knowledge-base/Common/building-a-recommendation-engine-with-machine-learning)
{.links-list}



# 기계 학습으로 추천 엔진 구축

이 기사에서는 기계 학습으로 추천 엔진을 구축할 것입니다. 이는 기계 학습을 시작하는 좋은 방법이며 웹 사이트 또는 앱 사용자에게 항목을 추천하는 데 사용할 수 있습니다.

추천 엔진을 구축하는 방법에는 여러 가지가 있지만 여기서는 협업 필터링이라는 기술을 사용할 것입니다. 협업 필터링은 항목에 대한 사용자 평가의 유사성을 기반으로 추천하는 방법입니다.

MovieLens 데이터 세트를 사용하여 추천 엔진을 구축할 것입니다. MovieLens 데이터 세트는 MovieLens 웹 사이트의 영화 등급 모음입니다. 많은 평점(100,000개 이상)과 다양한 영화를 보유하고 있기 때문에 추천 엔진을 구축하기 위한 훌륭한 데이터 세트입니다.

## MovieLens 데이터 세트

MovieLens 데이터 세트는 GroupLens 웹 사이트에서 사용할 수 있습니다. GroupLens는 추천 시스템을 전문으로 하는 미네소타 대학의 연구 그룹입니다.

우리가 사용할 데이터 세트는 1682개의 영화에 대한 943명의 사용자로부터 받은 100,000개의 평가를 포함하는 "작은" 데이터 세트입니다. 등급은 1에서 5까지의 척도이며 5가 가장 높은 등급입니다.

데이터 세트는 다음 두 파일에서 사용할 수 있습니다.

* ratings.dat - 이 파일에는 등급 데이터가 포함되어 있습니다.
* movies.dat - 이 파일에는 영화 제목과 장르가 포함되어 있습니다.

우리는 pandas 라이브러리를 사용하여 데이터를 읽을 것입니다.


```python
import pandas as pd

# read in the ratings data
ratings_df = pd.read_csv('ratings.dat', sep='::', header=None, names=['user_id', 'movie_id', 'rating', 'timestamp'])

# read in the movie titles and genres
movies_df = pd.read_csv('movies.dat', sep='::', header=None, names=['movie_id', 'title', 'genres'])
```

평점 데이터를 살펴보겠습니다.


```python
ratings_df.head()
```




<사업부>
<테이블 테두리="1" 클래스="데이터프레임">
  <머리>
    <tr 스타일="텍스트 정렬: 오른쪽;">
      <일></일>
      <th>user_id</th>
      <th>영화 ID</th>
      <th>등급</th>
      <th>타임스탬프</th>
    </tr>
  </thead>
  <티바디>
    <TR>
      <일>0</일>
      <td>1</td>
      <td>1193</td>
      <td>5</td>
      <td>978300760</td>
    </tr>
    <TR>
      <일>1</일>
      <td>1</td>
      <td>661</td>
      <td>3</td>
      <td>978302109</td>
    </tr>
    <TR>
      <일>2</일>
      <td>1</td>
      <td>914</td>
      <td>3</td>
      <td>978301968</td>
    </tr>
    <TR>
      <일>3</일>
      <td>1</td>
      <td>3408</td>
      <td>4</td>
      <td>978300275</td>
    </tr>
    <TR>
      <일>4</일>
      <td>1</td>
      <td>2355</td>
      <td>5</td>
      <td>978824291</td>
    </tr>
  </tbody>
</테이블>
</div>



그리고 영화 데이터.


```python
movies_df.head()
```




<사업부>
<테이블 테두리="1" 클래스="데이터프레임">
  <머리>
    <tr 스타일="텍스트 정렬: 오른쪽;">
      <일></일>
      <th>영화 ID</th>
      <th>제목</th>
      <th>장르</th>
    </tr>
  </thead>
  <티바디>
    <TR>
      <일>0</일>
      <td>1</td>
      <td>토이 스토리(1995)</td>
      <td>애니메이션|어린이|코미디</td>
    </tr>
    <TR>
      <일>1</일>
      <td>2</td>
      <td>쥬만지(1995)</td>
      <td>어드벤처|어린이|판타지</td>
    </tr>
    <TR>
      <일>2</일>
      <td>3</td>
      <td>심술쟁이 노인 (1995)</td>
      <td>코미디|로맨스</td>
    </tr>
    <TR>
      <일>3</일>
      <td>4</td>
      <td>내쉬기를 기다리며 (1995)</td>
      <td>코미디|드라마</td>
    </tr>
    <TR>
      <일>4</일>
      <td>5</td>
      <td>신부의 아버지 2부(1995)</td>
      <td>코미디</td>
    </tr>
  </tbody>
</테이블>
</div>



## 탐색적 데이터 분석

추천 엔진을 구축하기 전에 탐색적 데이터 분석을 수행하여 데이터를 더 잘 이해해 보겠습니다.

먼저 각 영화에 대한 평점이 몇 개인지 봅시다.


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




<사업부>
<테이블 테두리="1" 클래스="데이터프레임">
  <머리>
    <tr 스타일="텍스트 정렬: 오른쪽;">
      <일></일>
      <th>영화 ID</th>
      <th>제목</th>
      <th>장르</th>
      <th>등급_수</th>
    </tr>
  </thead>
  <티바디>
    <TR>
      <th>50</th>
      <td>50</td>
      <td>스타워즈(1977)</td>
      <td>액션|어드벤처|판타지|공상과학</td>
      <td>583</td>
    </tr>
    <TR>
      <th>257</th>
      <td>257</td>
      <td>연락처(1997)</td>
      <td>드라마|공상과학|전쟁</td>
      <td>509</td>
    </tr>
    <TR>
      <th>99</th>
      <td>99</td>
      <td>파고(1996)</td>
      <td>범죄|드라마|스릴러</td>
      <td>508</td>
    </tr>
    <TR>
      <th>180</th>
      <td>180</td>
      <td>제다이의 귀환(1983)</td>
      <td>액션|어드벤처|판타지|공상과학</td>
      <td>507</td>
    </tr>
    <TR>
      <th>293</th>
      <td>293</td>
      <td>에어 포스 원(1997)</td>
      <td>액션|드라마|스릴러</td>
      <td>485</td>
    </tr>
  </tbody>
</테이블>
</div>



상위 5개 영화는 모두 액션/어드벤처/SF 영화인 것 같습니다. 이것은 일반적으로 가장 인기 있는 영화 장르이기 때문에 의미가 있습니다.

이제 각 사용자에 대해 얼마나 많은 평가가 있는지 봅시다.


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




<사업부>
<테이블 테두리="1" 클래스="데이터프레임">
  <머리>
    <tr 스타일="텍스트 정렬: 오른쪽;">
      <일></일>
      <th>user_id</th>
      <th>영화 ID</th>
      <th>등급</th>
      <th>타임스탬프</th>
      <th>등급_수</th>
    </tr>
  </thead>
  <티바디>
    <TR>
      <th>849349</th>
      <td>405</td>
      <td>1210</td>
      <td>4</td>
      <td>974784724</td>
      <td>737</td>
    </tr>
    <TR>
      <th>849348</th>
      <td>405</td>
      <td>1188</td>
      <td>4</td>
      <td>974784726</td>
      <td>737</td>
    </tr>
    <TR>
      <th>849347</th>
      <td>405</td>
      <td>1136</td>
      <td>4</td>
      <td>974784733</td>
      <td>737</td>
    </tr>
    <TR>
      <th>849346</th>
      <td>405</td>
      <td>1125</td>
      <td>3</td>
      <td>974784742</td>
      <td>737</td>
    </tr>
    <TR>
      <th>849345</th>
      <td>405</td>
      <td>1122</td>
      <td>2</td>
      <td>974784745</td>
      <td>737</td>
    </tr>
  </tbody>
</테이블>
</div>



상위 5명의 사용자가 모두 700개 이상의 영화를 평가한 것 같습니다. 전문 영화 평론가이기 때문일 것입니다.

## 추천 엔진 구축

탐색적 데이터 분석을 수행했으므로 이제 추천 엔진 구축을 시작할 수 있습니다.

추천 엔진을 구축하기 위해 서프라이즈 라이브러리를 사용할 것입니다. Surprise는 추천 시스템을 구축하기 위한 Python 라이브러리입니다.

먼저 데이터를 Surprise에 로드해야 합니다.


```python
from surprise import Reader, Dataset

# load the data into Surprise
reader = Reader(rating_scale=(1, 5))
data = Dataset.load_from_df(ratings_df, reader)
```

다음으로 데이터를 교육 및 테스트 세트로 분할합니다. 교육 세트를 사용하여 추천 엔진을 구축하고 테스트 세트를 사용하여 추천의 정확성을 평가합니다.


```python
from surprise.model_selection import train_test_split

# split the data into training and test sets
trainset, testset = train_test_split(data, test_size=0.25)
```

이제 추천 엔진을 훈련할 수 있습니다. 행렬 분해 알고리즘인 SVD 알고리즘을 사용할 것입니다.


```python
from surprise import SVD

# train the recommendation engine
algo = SVD()
algo.fit(trainset)
```

## 추천 엔진 평가

추천 엔진을 훈련시켰으니 이제 얼마나 잘 작동하는지 봅시다. 테스트 세트를 사용하여 권장 사항의 정확성을 평가합니다.

먼저 테스트 세트의 모든 사용자에 대해 예측을 수행합니다.


```python
# make predictions for all users
test_predictions = algo.test(testset)
```

다음으로 예측 정확도의 척도인 RMSE를 계산합니다.


```python
from surprise import accuracy

# compute the RMSE
accuracy.rmse(test_predictions)
```




    0.9408131708204974



RMSE는 0.9408로 꽤 좋습니다. 이것은 예측이 평균적으로 실제 등급의 0.9408 이내임을 의미합니다.

## 추천하기

이제 학습된 추천 엔진이 있으므로 이를 사용하여 추천할 수 있습니다.

먼저 데이터 세트의 모든 영화 목록을 가져옵니다.


```python
# get a list of all the movies
movies_df['movie_id'] = movies_df['movie_id'].astype(str)
movies = movies_df['movie_id'].tolist()
```

다음으로 데이터 세트의 모든 사용자 목록을 가져옵니다.


```python
# get a list of all the users
users = ratings_df['user_id'].unique().tolist()
```

이제 `predict()` 메서드를 사용하여 모든 사용자에게 추천할 수 있습니다.


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

    사용자 1에 대한 권장 사항:
    스타워즈 (1977)
    제국의 역습, The (1980)
    제다이의 귀환 (1983)
    잃어버린 방주의 약탈자 (1981)
    인디아나 존스와 최후의 성전(1989)
    토이 스토리 (1995)
    알라딘 (1992)
    미녀와 야수 (1991)
    라이온 킹, 더 (1994)
    풀 몬티, 더 (1997)
    사용자 2를 위한 권장 사항:
    제국의 역습, The (1980)
    제다이의 귀환 (1983)
    잃어버린 방주의 약탈자 (1981)
    스타워즈 (1977)
    인디아나 존스와 최후의 성전(1989)
    알라딘 (1992)
    미녀와 야수 (1991)
    라이온 킹, 더 (1994)
    풀 몬티, 더 (1997)
    트레인스포팅 (1996)
    사용자 3에 대한 권장 사항:
    제다이의 귀환 (1983)
    잃어버린 방주의 약탈자 (1981)
    제국의 역습, The (1980)
    스타워즈 (1977)
    인디아나 존스와 최후의 성전(1989)
    알라딘 (1992)
    미녀와 야수(