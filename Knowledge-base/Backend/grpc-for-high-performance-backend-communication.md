---
title: 고성능 백엔드 통신을 위한 gRPC
description: 
published: true
date: 2023-02-17T18:13:24.700Z
tags: 
editor: markdown
dateCreated: 2023-01-30T20:43:33.201Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [gRPC for High-performance Backend Communication***English** version of this document is available*](/en/Knowledge-base/Backend/grpc-for-high-performance-backend-communication)
{.links-list}


# 소개

최근 몇 년 동안 gRPC는 백엔드 서비스를 위한 인기 있는 통신 프로토콜이 되었습니다. 모든 환경에서 실행할 수 있는 고성능 오픈 소스 RPC 프레임워크입니다. gRPC는 HTTP/2 프로토콜을 기반으로 하며 프로토콜 버퍼를 IDL(인터페이스 정의 언어)로 사용합니다.

gRPC는 빠르고 효율적이며 사용하기 쉽기 때문에 백엔드 서비스 간 통신에 적합합니다. 이 기사에서는 고성능 백엔드 통신을 위해 gRPC를 사용하는 방법을 살펴보겠습니다. 또한 시작하는 데 도움이 되는 몇 가지 샘플 코드 스니펫을 제공합니다.

# gRPC란?

gRPC는 모든 환경에서 실행할 수 있는 고성능 오픈 소스 RPC(원격 프로시저 호출) 프레임워크입니다. HTTP/2 프로토콜을 기반으로 하며 인터페이스 정의 언어(IDL)로 프로토콜 버퍼를 사용합니다.

gRPC는 고성능 백엔드 통신용으로 설계되었습니다. 효율적이고 사용하기 쉽습니다. gRPC를 사용하면 보다 효율적인 방식으로 데이터를 구성할 수 있으며 HTTP/2의 다중화 및 스트리밍 기능을 활용할 수도 있습니다.

# gRPC는 어떻게 사용하나요?

gRPC를 사용하는 것은 쉽습니다. 먼저 gRPC 도구 키트를 설치해야 합니다. https://grpc.io/docs/quickstart/installation/에서 설치 지침을 찾을 수 있습니다.

gRPC 도구 키트를 설치하면 모든 프로그래밍 언어로 코드를 작성할 수 있습니다. gRPC는 C++, Java, Python, Go를 비롯한 다양한 언어를 지원합니다.

이 기사에서는 Python을 사용합니다. 또한 프로토콜 버퍼 IDL을 사용하여 데이터 구조를 정의합니다.

# 데이터 구조 정의

첫 번째 단계는 프로토콜 버퍼를 사용하여 데이터 구조를 정의하는 것입니다. 프로토콜 버퍼는 사람이 읽을 수 있고 기계가 읽을 수 있는 방식으로 데이터 구조를 정의할 수 있는 언어 중립적이고 플랫폼 중립적인 IDL입니다.

다음은 사용자를 나타내는 데 사용할 수 있는 데이터 구조의 예입니다.

```protobuf
message User {
  string name = 1;
  string email = 2;
  int32 age = 3;
}
```

이 예에서는 User라는 데이터 구조를 정의했습니다. 이 데이터 구조에는 이름, 이메일 및 연령의 세 가지 필드가 있습니다. 각 필드 옆의 숫자는 필드의 식별자입니다.

# 서비스 정의

데이터 구조를 정의했으면 서비스를 정의해야 합니다. 서비스는 관련 RPC 메서드의 그룹입니다.

이 예제에서는 UserService라는 서비스를 정의합니다. 이 서비스에는 GetUser 및 CreateUser의 두 가지 방법이 있습니다.

```protobuf
service UserService {
  rpc GetUser (UserRequest) returns (UserResponse);
  rpc CreateUser (CreateUserRequest) returns (CreateUserResponse);
}

message UserRequest {
  User user = 1;
}

message UserResponse {
  User user = 1;
}

message CreateUserRequest {
  User user = 1;
}

message CreateUserResponse {
  User user = 1;
}
```

이 예제에서는 GetUser 및 CreateUser 메서드를 정의했습니다. 각 메서드는 요청 메시지를 받고 응답 메시지를 반환합니다.

# 서비스 구현

서비스를 정의했으면 구현해야 합니다. 이 예제에서는 Python을 사용하여 UserService를 구현합니다.

먼저 .proto 파일에서 Python 코드를 생성해야 합니다. 우리는 protoc 컴파일러를 사용하여 이것을 할 수 있습니다.

```
protoc -I=. --python_out=. user.proto
```

그러면 user_pb2.py라는 Python 파일이 생성됩니다. 이 파일에는 User 및 UserService 클래스에 대한 Python 코드가 포함되어 있습니다.

다음으로 UserService에 대한 코드를 작성해야 합니다. UserService라는 클래스를 정의하여 시작하겠습니다.

```python
class UserService(object):
  def __init__(self):
    self.users = {}
    
  def GetUser(self, user_request, context):
    user = self.users.get(user_request.user.id, None)
    if user is None:
      return user_pb2.UserResponse(error="User not found")
    return user_pb2.UserResponse(user=user)

  def CreateUser(self, user_request, context):
    user = user_request.user
    self.users[user.id] = user
    return user_pb2.CreateUserResponse(user=user)
```

이 예에서는 사용자를 위한 간단한 메모리 내 저장소를 정의했습니다. GetUser 및 CreateUser 메서드도 정의했습니다. 이 메서드는 요청 메시지를 받고 응답 메시지를 반환합니다.

# 서비스 제공

서비스를 구현한 후에는 클라이언트가 사용할 수 있도록 해야 합니다. 가장 쉬운 방법은 gRPC 서버를 사용하는 것입니다.

먼저 gRPC 서버를 만들어야 합니다. grpc-python 라이브러리를 사용하여 이 작업을 수행할 수 있습니다.

```python
import grpc

server = grpc.server(futures.ThreadPoolExecutor(max_workers=10))
```

다음으로 서버에 UserService를 추가해야 합니다.

```python
user_service = UserService()

user_pb2_grpc.add_UserServiceServicer_to_server(
    user_service, server)
```

마지막으로 서버를 시작해야 합니다.

```python
server.add_insecure_port('[::]:50051')
server.start()
server.wait_for_termination()
```

# 서비스 호출

이제 서비스가 실행 중이므로 클라이언트에서 호출할 수 있습니다. 이 예에서는 Python 클라이언트를 사용합니다.

먼저 서비스에 대한 Python 코드를 생성해야 합니다. 우리는 protoc 컴파일러를 사용하여 이것을 할 수 있습니다:

```
protoc -I=. --python_out=. user.proto
```

그러면 user_pb2.py라는 Python 파일이 생성됩니다. 이 파일에는 User 및 UserService 클래스에 대한 Python 코드가 포함되어 있습니다.

다음으로 서비스에 대한 스텁을 생성해야 합니다.

```python
channel = grpc.insecure_channel('localhost:50051')
stub = user_pb2_grpc.UserServiceStub(channel)
```

마지막으로 서비스 메서드를 호출할 수 있습니다.

```python
response = stub.GetUser(user_pb2.UserRequest(user=user))
print(response.user)

response = stub.CreateUser(user_pb2.CreateUserRequest(user=user))
print(response.user)
```

# 결론

이 기사에서는 고성능 백엔드 통신을 위해 gRPC를 사용하는 방법을 살펴보았습니다. 또한 시작하는 데 도움이 되는 몇 가지 샘플 코드 스니펫을 제공했습니다.