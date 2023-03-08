---
title: Understanding Load Balancing Techniques in Infrastructure Development
description: 
published: true
date: 2023-02-17T18:01:47.342Z
tags: 
editor: markdown
dateCreated: 2023-01-30T04:37:59.571Z
---

- [인프라 개발의 로드 밸런싱 기술 이해***Korean** version of this document is available*](/ko/Knowledge-base/Backend/understanding-load-balancing-techniques-in-infrastructure-development)
{.links-list}


# Load Balancing Techniques in Infrastructure Development

In today's world, data is processed in real time and at large scale. Users expect responsiveness and availability from the systems they use. Infrastructure must be able to handle the scale and load while providing the required level of responsiveness and availability.

Load balancing is a technique used to distribute workloads evenly across a network of computers so that no single computer is overloaded. By spreading the load, load balancing improves the overall performance of the network.

There are many types of load balancers, and the most appropriate type depends on the nature of the workload and the desired level of performance. The following are some of the most common types of load balancers:

## Round Robin

In this type of load balancer, each request is sent to the next computer in sequence. Round robin is a simple and widely used load balancing technique, but it does not account for each computer's processing time.

Round Robin is a simple and basic load balancing algorithm. It works by distributing incoming requests to a group of servers in a circular manner. It does not take into consideration the processing time of each server, so it may lead to some servers being over-utilized while others are under-utilized. The following is a simple example of Round Robin algorithm in Python.

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

* Least Connections: 

Least Connections is a more advanced load balancing algorithm. It works by sending incoming requests to the server that currently has the least number of active connections. This helps to balance the load evenly across all servers. The following is a simple example of Least Connections algorithm in Python.

With this type of load balancer, each request is sent to the computer with the fewest current connections. This ensures that the load is distributed evenly across all computers.

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

## Weighted Round Robin

With this type of load balancer, each request is sent to the next computer in the sequence, but the computers are given different weights depending on their processing power. This ensures that the load is distributed evenly across all computers.

Weighted Round Robin is a variant of the basic Round Robin algorithm. It allows administrators to assign different weights to each server based on their processing power. Servers with higher weights receive more requests compared to servers with lower weights. The following is a simple example of Weighted Round Robin algorithm in Python.

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

## Least Response Time

With this type of load balancer, each request is sent to the computer with the shortest response time. This ensures that the most responsive computers are used more often.

Least Response Time is a load balancing algorithm that selects the server with the shortest response time to handle incoming requests. It helps to ensure that requests are handled by the most responsive servers and reduces the response time for clients. The following is a simple example of Least Response Time algorithm in Python.

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

Note that the code examples provided are just for demonstration purposes and may not reflect the actual implementation in a real-world scenario. The actual implementation should take into consideration factors such as network latency, server utilization, and error handling.


The following are some factors to consider when choosing a load balancing technique:

* The nature of the workload: Some workloads are more suited to certain load balancing techniques than others. For example, a workload that is highly dependent on database access may be better suited to a round robin load balancer, while a workload that is more CPU-intensive may be better suited to a weighted round robin load balancer.

* The desired level of performance: The type of load balancer used will impact the performance of the system. Different load balancers have different performance characteristics, so it is important to choose a load balancer that is appropriate for the desired level of performance.

* The number of computers in the network: The type of load balancer used will also impact the scalability of the system. Some load balancers can only be used with a limited number of computers, while others can be used with a large number of computers.

Load balancing is a critical part of infrastructure development. By understanding the different types of load balancers and the factors to consider when choosing a load balancer, you can ensure that your infrastructure is able to handle the scale and load while providing the required level of responsiveness and availability.