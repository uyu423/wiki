---
title: Redis 데이터 구조: 알아야 할 사항
description: 
published: true
date: 2023-03-10T07:32:56.374Z
tags: 
editor: markdown
dateCreated: 2023-03-10T07:32:56.374Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Redis Data Structures: What You Need to Know***English** document is available*](/en/Knowledge-base/NoSQL/redis-data-structures-what-you-need-to-know)
{.links-list}

Redis 데이터 구조: 알아야 할 사항

Redis는 문자열, 해시, 목록, 세트 및 정렬된 세트와 같은 다양한 데이터 구조를 지원하는 인기 있는 오픈 소스 메모리 내 데이터 구조 저장소입니다. Redis 데이터 구조는 매우 효율적이고 빠르며 확장 가능하도록 설계되었으므로 Redis는 고성능 애플리케이션 구축에 이상적인 선택입니다. 이 기사에서는 가장 일반적인 Redis 데이터 구조와 실제 애플리케이션에서의 사용법을 살펴봅니다.

## Redis 문자열

Redis 문자열은 Redis에서 가장 기본적인 데이터 구조이며 바이너리 또는 텍스트 데이터를 저장할 수 있습니다. Redis 문자열의 최대 길이는 512MB입니다. Redis는 설정, 가져오기, 추가, 증분, 감소 등과 같은 문자열에 대한 많은 유용한 작업을 제공합니다.

다음은 Python에서 Redis 문자열을 사용하는 예입니다.

```python
import redis

r = redis.Redis(host='localhost', port=6379, db=0)

# set a string value
r.set('mykey', 'Hello World')

# get a string value
value = r.get('mykey')
print(value) # 'Hello World'

# increment a number
r.incr('counter')
value = r.get('counter')
print(value) # '1'
```

## 레디스 해시

Redis 해시는 키와 값이 문자열인 키-값 쌍의 모음입니다. Redis 해시는 사용자 프로필, 제품 정보 등과 같은 개체 또는 레코드를 나타내는 데 매우 유용합니다. Redis는 설정, 가져오기, 삭제, 증가, 감소 등과 같은 해시에 대한 많은 작업을 제공합니다.

다음은 Node.js에서 Redis 해시를 사용하는 예입니다.

```javascript
const redis = require('redis');
const client = redis.createClient();

// set a hash value
client.hset('user:1', 'name', 'John');
client.hset('user:1', 'age', 30);

// get a hash value
client.hgetall('user:1', function (err, obj) {
  console.log(obj); // { name: 'John', age: '30' }
});

// increment a hash field
client.hincrby('user:1', 'age', 1, function (err, value) {
  console.log(value); // 31
});
```

## 레디스 목록

Redis 목록은 각 문자열이 목록의 요소를 나타내는 문자열 모음입니다. Redis 목록은 로그, 메시지 등과 같이 순서가 지정된 데이터를 나타내는 데 매우 유용합니다. Redis는 푸시, 팝, 트림, 범위 등과 같은 목록에 대한 많은 작업을 제공합니다.

다음은 Ruby에서 Redis 목록을 사용하는 예입니다.

```ruby
require 'redis'
r = Redis.new

# push elements to a list
r.rpush('logs', 'message1', 'message2', 'message3')

# pop an element from the list
value = r.lpop('logs')
puts value # 'message1'

# get a range of elements from the list
values = r.lrange('logs', 0, -1)
puts values # ['message2', 'message3']
```

## 레디스 세트

Redis 세트는 고유한 문자열의 모음이며 각 문자열은 세트의 요소를 나타냅니다. Redis 세트는 팔로워, 좋아요 등과 같은 데이터 간의 관계를 나타내는 데 매우 유용합니다. Redis는 추가, 제거, 합집합, 교차 등과 같은 집합에 대한 많은 작업을 제공합니다.

다음은 PHP에서 Redis 세트를 사용하는 예입니다.

```php
$redis = new Redis();
$redis->connect('127.0.0.1', 6379);

// add elements to a set
$redis->sadd('likes:post1', 'user1', 'user2', 'user3');
$redis->sadd('likes:post2', 'user2', 'user3', 'user4');

// get the union of two sets
$users = $redis->sunion('likes:post1', 'likes:post2');
print_r($users); // Array ( [0] => user1 [1] => user2 [2] => user3 [3] => user4 )
```

## Redis 정렬 세트

Redis 정렬 세트는 Redis 세트와 유사하지만 정렬 세트의 각 요소는 점수와 연결됩니다. Redis 정렬 세트는 순위표, 순위 등과 같은 점수로 정렬된 데이터를 나타내는 데 매우 유용합니다. Redis는 추가, 제거, 순위 지정, 범위 지정 등과 같은 정렬된 집합에 대한 많은 작업을 제공합니다.

다음은 Go에서 Redis 정렬 집합을 사용하는 예입니다.

```go
package main

import "github.com/go-redis/redis"

func main() {
    client := redis.NewClient(&redis.Options{
        Addr: "localhost:6379",
        Password: "",
        DB: 0,
    })

    // add elements to a sorted set
    client.ZAdd("leaderboard", &redis.Z{Score: 100, Member: "player1"})
    client.ZAdd("leaderboard", &redis.Z{Score: 200, Member: "player2"})
    client.ZAdd("leaderboard", &redis.Z{Score: 50, Member: "player3"})

    // get the top players
    players, err := client.ZRevRangeWithScores("leaderboard", 0, 1).Result()
    if err != nil {
        panic(err)
    }
    for _, p := range players {
        println(p.Member, p.Score)
    }
}
```

## 결론

Redis 데이터 구조는 효율적이고 확장 가능한 데이터 스토리지로 고성능 애플리케이션을 구축하기 위한 강력한 도구입니다. Redis는 문자열, 해시, 목록, 세트 및 정렬된 세트와 같은 다양한 데이터 구조를 제공하며, 각 세트에는 효율적인 데이터 조작을 위한 고유한 작업 세트가 있습니다. 다양한 Redis 데이터 구조와 실제 애플리케이션에서의 사용법을 이해하면 더 빠르고 안정적인 애플리케이션을 구축할 수 있습니다.

## 외부 리소스

- [레디스 문서](https://redis.io/documentation)
- [Redis 데이터 유형](https://redis.io/topics/data-types)
- [레디스 명령어](https://redis.io/commands)