---
title: ハイパフォーマンスなバックエンド通信のための gRPC
description: 
published: true
date: 2023-02-17T18:13:26.658Z
tags: 
editor: markdown
dateCreated: 2023-01-30T20:43:33.201Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [gRPC for High-performance Backend Communication***English** version of this document is available*](/en/Knowledge-base/Backend/grpc-for-high-performance-backend-communication)
{.links-list}


#はじめに

近年、gRPCはバックエンドサービスのための人気のある通信プロトコルになりました。あらゆる環境で実行できる高性能オープンソースRPCフレームワークです。 gRPCはHTTP / 2プロトコルに基づいており、プロトコルバッファをインターフェース定義言語（IDL）として使用します。

gRPCは高速で効率的で使いやすいので、バックエンドサービス間の通信に適しています。この記事では、高性能バックエンド通信にgRPCを使用する方法について説明します。また、始めるのに役立ついくつかのサンプルコードスニペットも提供しています。

#gRPCとは何ですか？

gRPCは、あらゆる環境で実行できる高性能オープンソースリモートプロシージャコール（RPC）フレームワークです。 HTTP/2 プロトコルに基づいており、インターフェイス定義言語 (IDL) でプロトコルバッファを使用します。

gRPCは、高性能バックエンド通信用に設計されています。効率的で使いやすいです。 gRPCを使用すると、より効率的な方法でデータを整理でき、HTTP / 2の多重化およびストリーミング機能を活用できます。

# gRPCはどのように使用しますか？

gRPCを使用するのは簡単です。まず、gRPCツールキットをインストールする必要があります。 https://grpc.io/docs/quickstart/installation/でインストール手順を見つけることができます。

gRPCツールキットをインストールすると、任意のプログラミング言語でコードを書くことができます。 gRPCはC ++、Java、Python、Goなどのさまざまな言語をサポートしています。

この記事ではPythonを使用します。また、プロトコルバッファIDLを使用してデータ構造を定義します。

# データ構造の定義

最初のステップは、プロトコルバッファを使用してデータ構造を定義することです。プロトコルバッファは、人間が読み取ることができ、機械が読み取ることができる方法でデータ構造を定義できる言語中立的でプラットフォーム中立的なIDLです。

以下は、ユーザーを表すために使用できるデータ構造の例です。

``protobuf
message User {
  string name = 1;
  string email = 2;
  int32 age = 3;
}
```

この例では、Userというデータ構造を定義しました。このデータ構造には、名前、電子メール、年齢の3つのフィールドがあります。各フィールドの横の数字はフィールドの識別子です。

# サービス定義

データ構造を定義したら、サービスを定義する必要があります。サービスは、関連する RPC メソッドのグループです。

この例では、UserService というサービスを定義します。このサービスには、GetUserとCreateUserの2つの方法があります。

``protobuf
service UserService {
  rpc GetUser(UserRequest) returns(UserResponse);
  rpc CreateUser(CreateUserRequest) returns(CreateUserResponse);
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

この例では、GetUser メソッドと CreateUser メソッドを定義しました。各メソッドは要求メッセージを受け取り、応答メッセージを返します。

# サービスの実装

サービスを定義したら、実装する必要があります。この例では、Pythonを使用してUserServiceを実装しています。

まず、.protoファイルからPythonコードを生成する必要があります。私たちはプロトコンパイラを使ってこれを行うことができます。

```
protoc -I=。 --python_out=。 user.proto
```

これにより、user_pb2.pyというPythonファイルが作成されます。このファイルには、UserクラスとUserServiceクラスのPythonコードが含まれています。

次に、UserServiceのコードを記述する必要があります。 UserServiceというクラスを定義して始めましょう。

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
    user=user_request.user
    self.users[user.id] = user
    return user_pb2.CreateUserResponse(user=user)
```

この例では、ユーザーのための単純なインメモリストレージを定義しました。 GetUser メソッドと CreateUser メソッドも定義しました。このメソッドは要求メッセージを受け取り、応答メッセージを返します。

#サービス提供

サービスを実装したら、クライアントが利用できるようにする必要があります。最も簡単な方法はgRPCサーバーを使用することです。

まず、gRPCサーバーを作成する必要があります。 grpc-pythonライブラリを使用してこれを行うことができます。

```python
import grpc

server = grpc.server(futures.ThreadPoolExecutor(max_workers=10))
```

次に、サーバーにUserServiceを追加する必要があります。

```python
user_service = UserService()

user_pb2_grpc.add_UserServiceServicer_to_server(
    user_service, server)
```

最後にサーバーを起動する必要があります。

```python
server.add_insecure_port('[::]:50051')
server.start()
server.wait_for_termination()
```

# サービスコール

これでサービスが実行されているため、クライアントから呼び出すことができます。この例ではPythonクライアントを使用しています。

まず、サービスのPythonコードを生成する必要があります。私たちはprotocコンパイラを使ってこれを行うことができます：

```
protoc -I=。 --python_out=。 user.proto
```

これにより、user_pb2.pyというPythonファイルが作成されます。このファイルには、UserクラスとUserServiceクラスのPythonコードが含まれています。

次に、サービスのスタブを作成する必要があります。

```python
channel = grpc.insecure_channel('localhost:50051')
stub = user_pb2_grpc.UserServiceStub(channel)
```

最後に、サービスメソッドを呼び出すことができます。

```python
response = stub.GetUser(user_pb2.UserRequest(user=user))
print(response.user)

response = stub.CreateUser(user_pb2.CreateUserRequest(user=user))
print(response.user)
```

#結論

この記事では、高性能バックエンド通信にgRPCを使用する方法について説明しました。また、始めるのに役立ついくつかのサンプルコードスニペットを提供しました。