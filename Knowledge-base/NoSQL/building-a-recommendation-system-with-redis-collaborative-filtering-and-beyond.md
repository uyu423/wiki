---
title: Redis로 추천 시스템 구축: 협업 필터링 및 그 이상
description: 
published: true
date: 2023-03-06T22:33:11.231Z
tags: 
editor: markdown
dateCreated: 2023-03-06T22:33:03.874Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Building a Recommendation System with Redis: Collaborative Filtering and Beyond***English** document is available*](/en/Knowledge-base/NoSQL/building-a-recommendation-system-with-redis-collaborative-filtering-and-beyond)
{.links-list}



Redis로 추천 시스템 구축: 협업 필터링 및 그 이상

소개

추천 시스템은 Netflix에서 영화를 제안하는 것부터 Amazon이 제품을 추천하는 것에 이르기까지 현대 비즈니스의 중요한 측면이 되었습니다. 추천 시스템은 과거의 선호도와 행동을 기반으로 사용자의 선호도를 예측하는 일종의 정보 필터링 시스템입니다.

Redis는 데이터베이스, 캐시 및 메시지 브로커로 사용할 수 있는 오픈 소스 메모리 내 데이터 구조 저장소입니다. 정렬된 집합, 목록 및 해시와 같은 여러 기능을 제공하므로 추천 시스템을 구축하는 데 탁월한 선택입니다.

이 기사에서는 Redis를 사용하여 추천 시스템을 구축하는 방법을 살펴봅니다. 추천 시스템 구축에 널리 사용되는 알고리즘인 협업 필터링에 초점을 맞추고 시스템 성능을 개선하는 데 사용할 수 있는 몇 가지 고급 기술을 탐구합니다.

협업 필터링

협업 필터링은 많은 사용자의 선호도를 사용하여 다른 사용자에게 항목을 추천하는 기술입니다. 유사한 선호도를 가진 사용자를 식별하고 이러한 사용자가 좋아하는 항목을 추천하는 방식으로 작동합니다.

협업 필터링에는 사용자 기반 및 항목 기반의 두 가지 유형이 있습니다. 사용자 기반 협업 필터링은 유사한 다른 사용자의 선호도를 기반으로 사용자에게 항목을 추천합니다. 반면 아이템 기반 협업 필터링은 사용자가 과거에 좋아했던 아이템의 유사성을 기반으로 아이템을 추천합니다.

이 기사에서는 사용자 기반 협업 필터링 접근 방식에 중점을 둘 것입니다.

Redis로 추천 시스템 구축

Redis를 사용하여 추천 시스템 구축에 필요한 데이터를 저장합니다. 특히 정렬된 세트를 사용하여 사용자 항목 등급 및 항목 유사성을 저장합니다.

1단계: 데이터 수집 및 저장

추천 시스템 구축의 첫 번째 단계는 데이터 수집 및 저장입니다. 이 경우 영화 등급 데이터 세트를 사용합니다. 데이터 세트에는 1에서 5까지의 등급으로 사용자의 영화 평가가 포함되어 있습니다.

정렬된 세트를 사용하여 Redis에 등급을 저장합니다. 각 사용자는 자신이 평가한 모든 영화의 등급을 포함하는 정렬된 집합과 연결됩니다. 영화 ID는 정렬된 집합의 구성원이며 등급은 점수입니다.

```redis
ZADD user:1 5 movie:1
ZADD user:1 4 movie:2
ZADD user:1 3 movie:3
```

위의 예에서는 사용자 1의 영화 1, 2, 3 등급을 Redis에 추가하고 있습니다.

2단계: 유사성 계산

다음 단계는 항목 간의 유사성을 계산하는 것입니다. 협업 필터링에 사용되는 인기 있는 유사성 메트릭인 Pearson 상관 계수를 사용합니다.

두 항목을 모두 평가한 모든 사용자가 부여한 등급을 비교하여 두 항목 간의 유사성을 계산합니다. 정렬된 세트를 사용하여 항목 간의 유사성을 저장합니다. 각 항목은 다른 항목과의 유사성을 포함하는 정렬된 집합과 연결됩니다. 다른 항목 ID는 정렬된 집합의 구성원이며 유사성은 점수입니다.

```python
def calculate_similarity(item1, item2):
    users1 = redis.zrevrangebyscore(f"item:{item1}", "+inf", "-inf")
    users2 = redis.zrevrangebyscore(f"item:{item2}", "+inf", "-inf")
    users_both = set(users1).intersection(users2)
    n = len(users_both)
    if n == 0:
        return 0
    sum1 = sum([float(redis.zscore(f"user:{user}", f"item:{item1}")) for user in users_both])
    sum2 = sum([float(redis.zscore(f"user:{user}", f"item:{item2}")) for user in users_both])
    sum1_sq = sum([pow(float(redis.zscore(f"user:{user}", f"item:{item1}")), 2) for user in users_both])
    sum2_sq = sum([pow(float(redis.zscore(f"user:{user}", f"item:{item2}")), 2) for user in users_both])
    p_sum = sum([float(redis.zscore(f"user:{user}", f"item:{item1}")) * float(redis.zscore(f"user:{user}", f"item:{item2}")) for user in users_both])
    num = p_sum - (sum1 * sum2 / n)
    den = sqrt((sum1_sq - pow(sum1, 2) / n) * (sum2_sq - pow(sum2, 2) / n))
    if den == 0:
        return 0
    return num / den

similarity = calculate_similarity(1, 2)
redis.zadd(f"item:{1}", {2: similarity})
redis.zadd(f"item:{2}", {1: similarity})
```

위의 예에서는 항목 1과 2 사이의 유사도를 계산하여 Redis에 저장하고 있습니다.

3단계: 추천 생성

마지막 단계는 사용자를 위한 권장 사항을 생성하는 것입니다. 우리는 주어진 사용자와 유사한 사용자를 식별하고 이러한 사용자가 높게 평가한 항목을 추천함으로써 이를 수행합니다.

다음 알고리즘을 사용하여 권장 사항을 생성합니다.

1. 주어진 사용자의 등급을 가져옵니다.
2. 주어진 사용자와 유사한 사용자를 찾습니다.
3. 이 사용자의 최고 등급 항목을 가져옵니다.
4. 주어진 사용자가 평가하지 않았지만 유사한 사용자가 높은 평가를 한 항목을 추천하십시오.

```python
def recommend(user):
    # Get the ratings of the given user
    user_ratings = redis.zrangebyscore(f"user:{user}", "-inf", "+inf", withscores=True)
    rated_items = set([r[0] for r in user_ratings])
    # Find similar users
    similar_users = set()
    for item in rated_items:
        similar_items = redis.zrangebyscore(f"item:{item}", "+inf", "-inf")
        for similar_item in similar_items:
            if similar_item != item:
                similar_users |= set(redis.zrangebyscore(f"item:{similar_item}", "+inf", "-inf"))
    # Get top-rated items of similar users
    recommendations = []
    for similar_user in similar_users:
        if similar_user == user:
            continue
        similar_user_ratings = redis.zrangebyscore(f"user:{similar_user}", "4", "+inf")
        for rating in similar_user_ratings:
            item = rating.split(":")[1]
            if item not in rated_items:
                recommendations.append((item, float(rating.split(":")[0])))
                if len(recommendations) > 10:
                    break
        if len(recommendations) > 10:
            break
    # Return top N recommendations
    return sorted(recommendations, key=lambda x: x[1], reverse=True)[:10]

recommendations = recommend(1)
```

위의 예에서는 위에서 설명한 알고리즘을 사용하여 사용자 1에 대한 권장 사항을 생성합니다.

고급 기술

추천 시스템의 성능을 향상시키는 데 사용할 수 있는 몇 가지 고급 기술이 있습니다. 이 섹션에서는 행렬 분해 및 하이브리드 추천 시스템이라는 두 가지 기술을 살펴봅니다.

행렬 분해

행렬 분해는 큰 사용자 항목 등급 행렬의 차원을 줄이는 데 사용되는 기술입니다. 매트릭스를 두 개의 저차원 매트릭스로 분해하여 작동합니다. 하나는 사용자를 나타내고 다른 하나는 항목을 나타냅니다.

추천 시스템에서 흔히 볼 수 있는 희소 행렬을 처리하는 데 행렬 분해를 사용할 수 있습니다. 또한 데이터에서 명시적으로 사용할 수 없는 잠재 기능을 검색하는 데 사용할 수도 있습니다.

SVD(Singular Value Decomposition) 알고리즘을 사용하여 행렬 분해를 수행할 수 있습니다. 그런 다음 결과 매트릭스를 사용하여 권장 사항을 생성할 수 있습니다.

하이브리드 추천 시스템

하이브리드 추천 시스템은 여러 추천 기법을 결합하여 보다 정확하고 다양한 추천을 제공합니다. 아이디어는 다른 기술의 강점을 사용하고 약점을 극복하는 것입니다.

예를 들어 협업 필터링과 콘텐츠 기반 필터링을 결합할 수 있습니다. 컨텐츠 기반 필터링은 속성을 기반으로 항목을 추천하고 협업 필터링은 사용자 선호도를 기반으로 항목을 추천합니다. 이 두 가지 기술을 결합하여 정확하고 다양한 추천을 제공할 수 있습니다.

결론

이 기사에서는 Redis를 사용하여 추천 시스템을 구축하는 방법을 살펴보았습니다. 우리는 추천 시스템 구축에 널리 사용되는 알고리즘인 협업 필터링에 중점을 두었습니다. 또한 추천 시스템의 성능을 개선하는 데 사용할 수 있는 몇 가지 고급 기술을 살펴보았습니다.

추천 시스템 구축은 실험과 조정이 필요한 반복 프로세스입니다. 다양한 기술을 결합하고 특정 사용 사례에 적용함으로써 사용자와 비즈니스의 요구를 충족하는 추천 시스템을 구축할 수 있습니다.

외부 자원

- 레디스 문서: https://redis.io/documentation
- 협업 필터링: https://en.wikipedia.org/wiki/Collaborative_filtering
- 행렬 분해: https://en.wikipedia.org/wiki/Matrix_factorization_(recommender_systems)
- 하이브리드 추천 시스템: https://en.wikipedia.org/wiki/Hybrid_recommender_system