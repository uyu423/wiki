---
title: 인프라 개발의 로드 밸런싱 기술 이해
description: 
published: true
date: 2023-02-17T18:01:48.651Z
tags: 
editor: markdown
dateCreated: 2023-01-30T04:37:59.573Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Understanding Load Balancing Techniques in Infrastructure Development***English** version of this document is available*](/en/Knowledge-base/Backend/understanding-load-balancing-techniques-in-infrastructure-development)
{.links-list}


# 인프라 개발의 로드 밸런싱 기술

오늘날 세계에서 데이터는 실시간으로 대규모로 처리됩니다. 사용자는 사용하는 시스템에서 응답성과 가용성을 기대합니다. 인프라는 필요한 수준의 응답성과 가용성을 제공하면서 규모와 로드를 처리할 수 있어야 합니다.

로드 밸런싱은 단일 컴퓨터가 과부하되지 않도록 컴퓨터 네트워크 전체에 워크로드를 고르게 분배하는 데 사용되는 기술입니다. 로드를 분산함으로써 로드 밸런싱은 네트워크의 전반적인 성능을 향상시킵니다.

많은 유형의 로드 밸런서가 있으며 가장 적합한 유형은 워크로드의 특성과 원하는 성능 수준에 따라 다릅니다. 다음은 가장 일반적인 로드 밸런서 유형 중 일부입니다.

## 라운드 로빈

이 유형의 로드 밸런서에서는 각 요청이 순서대로 다음 컴퓨터로 전송됩니다. 라운드 로빈은 간단하고 널리 사용되는 로드 밸런싱 기술이지만 각 컴퓨터의 처리 시간을 고려하지는 않습니다.

라운드 로빈은 간단하고 기본적인 로드 밸런싱 알고리즘입니다. 들어오는 요청을 순환 방식으로 서버 그룹에 배포하여 작동합니다. 각 서버의 처리 시간을 고려하지 않으므로 일부 서버는 과도하게 사용되는 반면 다른 서버는 충분히 사용되지 않을 수 있습니다. 다음은 Python에서 라운드 로빈 알고리즘의 간단한 예입니다.

```python
servers = ['A', 'B', 'C']
index = 0

def get_server():
    global index
    server = servers[index]
    index = (index + 1) % len(servers)
    return server

# Example usage
requests = ['r1', 'r2', 'r3', 'r4', 'r5']
for request in requests:
    server = get_server()
    print(f"Request {request} is sent to server {server}")

# Output:
# Request r1 is sent to server A
# Request r2 is sent to server B
# Request r3 is sent to server C
# Request r4 is sent to server A
# Request r5 is sent to server B
```

## 최소 연결:

최소 연결은 고급 로드 밸런싱 알고리즘입니다. 현재 활성 연결 수가 가장 적은 서버에 들어오는 요청을 보내는 방식으로 작동합니다. 이렇게 하면 모든 서버에서 부하를 고르게 분산하는 데 도움이 됩니다. 다음은 Python의 최소 연결 알고리즘의 간단한 예입니다.

이 유형의 로드 밸런서에서는 각 요청이 현재 연결 수가 가장 적은 컴퓨터로 전송됩니다. 이렇게 하면 부하가 모든 컴퓨터에 고르게 분산됩니다.

```python
servers = [('A', 0), ('B', 0), ('C', 0)]

def get_server():
    server = min(servers, key=lambda x: x[1])
    server_name = server[0]
    server[1] += 1
    return server_name

# Example usage
requests = ['r1', 'r2', 'r3', 'r4', 'r5']
for request in requests:
    server = get_server()
    print(f"Request {request} is sent to server {server}")

# Output:
# Request r1 is sent to server A
# Request r2 is sent to server B
# Request r3 is sent to server C
# Request r4 is sent to server A
# Request r5 is sent to server B
```

## 가중 라운드 로빈

이 유형의 로드 밸런서에서는 각 요청이 순서대로 다음 컴퓨터로 전송되지만 처리 능력에 따라 컴퓨터에 다른 가중치가 부여됩니다. 이렇게 하면 부하가 모든 컴퓨터에 고르게 분산됩니다.

가중 라운드 로빈은 기본 라운드 로빈 알고리즘의 변형입니다. 이를 통해 관리자는 처리 능력에 따라 각 서버에 다른 가중치를 할당할 수 있습니다. 가중치가 높은 서버는 가중치가 낮은 서버에 비해 더 많은 요청을 받습니다. 다음은 Python의 Weighted Round Robin 알고리즘의 간단한 예입니다.

```python
servers = [('A', 1), ('B', 2), ('C', 3)]

def get_server():
    total_weight = sum([weight for _, weight in servers])
    random_num = random.uniform(0, total_weight)
    for name, weight in servers:
        random_num -= weight
        if random_num <= 0:
            return name

# Example usage
requests = ['r1', 'r2', 'r3', 'r4', 'r5']
for request in requests:
    server = get_server()
    print(f"Request {request} is sent to server {server}")

# Output:
# Request r1 is sent to server C
# Request r2 is sent to server A
# Request r3 is sent to server B
# Request r4 is sent to server C
# Request r5 is sent to server A
```

## 최소 응답 시간

이 유형의 로드 밸런서에서는 각 요청이 응답 시간이 가장 짧은 컴퓨터로 전송됩니다. 이렇게 하면 가장 반응이 빠른 컴퓨터를 더 자주 사용할 수 있습니다.

최소 응답 시간은 수신 요청을 처리하기 위해 응답 시간이 가장 짧은 서버를 선택하는 로드 밸런싱 알고리즘입니다. 응답이 가장 빠른 서버에서 요청을 처리하고 클라이언트의 응답 시간을 줄이는 데 도움이 됩니다. 다음은 Python의 최소 응답 시간 알고리즘의 간단한 예입니다.

```python
servers = [('A', 0), ('B', 0), ('C', 0)]

def get_server():
    server_times = []
    for name, response_time in servers:
        # mock the calculation of response time
        response_time = response_time + 1
        server_times.append((name, response_time))
    server = min(server_times, key=lambda x: x[1])
    server_name = server[0]
    return server_name

# Example usage
requests = ['r1', 'r2', 'r3', 'r4', 'r5']
for request in requests:
    server = get_server()
    print(f"Request {request} is sent to server {server}")

# Output:
# Request r1 is sent to server A
# Request r2 is sent to server B
# Request r3 is sent to server C
# Request r4 is sent to server A
# Request r5 is sent to server B
```

제공된 코드 예제는 데모용이며 실제 시나리오의 실제 구현을 반영하지 않을 수 있습니다. 실제 구현에서는 네트워크 대기 시간, 서버 활용도 및 오류 처리와 같은 요소를 고려해야 합니다.

다음은 부하 분산 기술을 선택할 때 고려해야 할 몇 가지 요소입니다.

* 워크로드의 특성: 일부 워크로드는 다른 것보다 특정 로드 밸런싱 기술에 더 적합합니다. 예를 들어 데이터베이스 액세스에 대한 의존도가 높은 워크로드는 라운드 로빈 로드 밸런서에 더 적합할 수 있는 반면 CPU 집약적인 워크로드는 가중 라운드 로빈 로드 밸런서에 더 적합할 수 있습니다.

* 원하는 성능 수준: 사용되는 로드 밸런서 유형은 시스템 성능에 영향을 미칩니다. 로드 밸런서마다 성능 특성이 다르므로 원하는 성능 수준에 적합한 로드 밸런서를 선택하는 것이 중요합니다.

* 네트워크의 컴퓨터 수: 사용되는 로드 밸런서 유형도 시스템의 확장성에 영향을 미칩니다. 일부 로드 밸런서는 제한된 수의 컴퓨터에서만 사용할 수 있는 반면 다른 로드 밸런서는 많은 수의 컴퓨터에서 사용할 수 있습니다.

로드 밸런싱은 인프라 개발의 중요한 부분입니다. 다양한 유형의 로드 밸런서와 로드 밸런서를 선택할 때 고려해야 할 요소를 이해하면 필요한 수준의 응답성과 가용성을 제공하면서 인프라가 규모와 로드를 처리할 수 있는지 확인할 수 있습니다.