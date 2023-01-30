---
title: Spring Boot のコマンド クエリ責任分離 (CQRS) パターン
description: 
published: true
date: 2023-01-30T22:05:07.464Z
tags: 
editor: markdown
dateCreated: 2023-01-30T22:05:07.464Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [The Command Query Responsibility Segregation (CQRS) Pattern in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/the-command-query-responsibility-segregation-cqrs-pattern-in-spring-boot)
{.links-list}


#Spring BootのCommand Query Responsibility Segregation（CQRS）パターン

CQRS（Command Query Responsibility Segregation）は、データ読み取りモデルとデータ書き込みモデルを区別するアーキテクチャパターンです。これらの問題の分離は、拡張性、パフォーマンス、およびメンテナンス性の向上など、多くの利点を提供できます。

この記事では、Spring BootアプリケーションでCQRSパターンを実装する方法について説明します。 CQRSパターンとコアコンセプトを簡単に紹介することから始めましょう。次に、Spring Bootを使用して単純なCQRSベースのアプリケーションを設定する方法を見てみましょう。最後に、Spring BootアプリケーションでCQRSを使用するためのいくつかのベストプラクティスを見てみましょう。

## CQRSについて

前述したように、CQRS パターンはデータ読み出しモデルとデータ書き込みモデルを分離します。従来のアプリケーションでは、これら2つのモデルはしばしば密接に結合されており、アプリケーションを拡張したりデータモデルを変更したりするのが難しい場合があります。

読み取りおよび書き込みモデルを分離することで、CQRSは各モデルを独立して拡張できます。たとえば、書き込みモデルではなく読み取りモデルに別のデータベースを使用できます。書込みモデルではなく読取りモデルに別のデータ構造を使用することもできます。この柔軟性により、CQRSベースのアプリケーションをはるかに簡単に拡張できます。

さらに、CQRSを使用すると、データモデルをより簡単に変更できます。たとえば、読み取りモデルに新しいフィールドを追加する必要がある場合は、書き込みモデルに影響を与えることなく追加できます。これにより、時間の経過とともにデータモデルをさらに簡単に開発できます。

## Spring BootでCQRSを実装する

CQRSパターンの高度な概要を見てきたので、Spring Bootアプリケーションでこれを実装する方法を見てみましょう。

メモリ内データベース（H2）を使用する単純なSpring Bootアプリケーションの作成から始めましょう。これは私たちの書き込みモデルになります。次に、読み取りモデル用に2番目のインメモリデータベース（HSQLDB）を追加します。最後に、読み取りモデルを照会するための単純なREST APIを追加します。

###書き込みモデル

書き込みモデル用の単純なエンティティを作成することから始めましょう。このエンティティは「ユーザー」です。

「Java
@リアル
公開クラスのユーザー{

    @ID
    @GeneratedValue
    個人の長いID;

    プライベート文字列名

    プライベートストリング城

    // ... ゲッターとセッター
}
```

次へ、私はリポジトリの「ユーザー」「for our」「ユーザー」のエンティティを作成します。 We'll use this repository to perform CRUD operations on our ```User '' entity.

「Java
パブリック インターフェイス UserRepository 拡張 JpaRepository<User, Long> {
}
```

Finally、we'll create a simple service ```User '' ' that uses our repository to create, read, update, and delete '' User '' entities。

「Java
@サービス
パブリッククラスUserService {

    @Autowired
    プライベートUserRepository userRepository;

    公開ユーザーcreateUser（ユーザーユーザー）{
        return userRepository.save（ユーザー）;
    }

    公開ユーザーgetUser（長いID）{
        return userRepository.findById(id).orElse(null);
    }

    公開ユーザー updateUser (ユーザーユーザー) {
        return userRepository.save（ユーザー）;
    }

    パブリック無効 deleteUser (ユーザー ユーザー) {
        userRepository.delete（ユーザー）;
    }
}
```

### Read Model

Now that we have our write model set up, let's create our read model. For our read model, we'll create a simple ```User '' ` class that contains the same fields as our ```User '' entity。

「Java
パブリッククラスUserDto {

    個人の長いID;
    プライベート文字列名
    プライベートストリング城
    
    // ... ゲッターとセッター
}
```

Next、we'll create a repository「UserDto」、 for our「UserDto」クラス。 We'll use this repository to query the read model.

「Java
パブリック インターフェイス UserDtoRepository 拡張 JpaRepository<UserDto, Long> {
}
```

Finally、we'll create a simple service ```UserDtoService ```' that uses our repository to query the read model.

「Java
@サービス
パブリック クラス UserDtoService {

    @Autowired
    プライベートUserDtoRepository userDtoRepository;

    公開リスト<UserDto> getAllUsers() {
        return userDtoRepository.findAll();
    }

    公開 UserDto getUser(Long id) {
        return userDtoRepository.findById(id).orElse(null);
    }
}
```

### REST API

Now that we have our write model and read model set up, let's create a simple REST API for querying the read model. We'll start by creating a controller ```GET '' with a ```GET '' endpoint for querying the read model.

「Java
@RestController
@RequestMapping("/ユーザー")
パブリッククラスUserController {

    @Autowired
    プライベートUserDtoService userDtoService;

    @GetMapping
    公開リスト<UserDto> getAllUsers() {
        return userDtoService.getAllUsers();
    }

    @GetMapping("/{id}")
    公開 UserDto getUser(@PathVariable Long id) {
        return userDtoService.getUser(id);
    }
}
```

Now that we have our controller set up, let's test it out. First, let's start our application and make sure that it's up and running.

Next、we'll create a few ```UserService ''、 ``entitysing our ```UserService ''。

「Java
ユーザーuser1 =新しいユーザー（）;
user1.setFirstName("ゾーン");
user1.setLastName("スミス");

ユーザーuser2 =新しいユーザー（）;
user2.setFirstName("ジェーン");
user2.setLastName("未来");

userService.createUser（ユーザー1）;
userService.createUser(user2);
```

Finally、we'll query our ```UserController '' to make sure that our ```UserDto '' 'entity were created correctly.

「Java
List<UserDto> users = userController.getAllUsers();

assertThat（ユーザー）。hasSize（2）;
assertThat(users.get(0).getFirstName()).isEqualTo("ゾーン");
assertThat(users.get(0).getLastName()).isEqualTo("スミス");
assertThat(users.get(1).getFirstName()).isEqualTo("ジェーン");
assertThat(users.get(1).getLastName()).isEqualTo("Doe");
```

## Best Practices

Now that we've seen how to implement the CQRS pattern in a Spring Boot application, let's look at some best practices for using CQRS in a Spring Boot application.

### Use a Messaging System

One best practice for using CQRS in a Spring Boot application is to use a messaging system. A messaging system can provide various benefits, such as improved scalability and performance.

There are many different messaging systems available, such as Apache Kafka and RabbitMQ. In this example, we'll use Apache Kafka.

First、we'll add the following dependencies to our ```pom.xml ```file：

```xml
<依存性>
    <groupId>org.springframework.kafka</groupId>
    <artifactId>スプリングカフカ</artifactId>
</依存性>

<依存性>
    <groupId>org.apache.kafka</groupId>
    <artifactId>カフカクライアント</artifactId>
</依存性>
```

次へ、私たちは通常の「メッセージプロデューサー」を公開しています。

「Java
@要素
パブリック クラス MessageProducer {

    @Autowired
    プライベートKafkaTemplate <文字列、文字列> kafkaTemplate;

    パブリック無効sendMessage（文字列トピック、文字列メッセージ）{
        kafkaTemplate.send（トピック、メッセージ）;
    }
}
```

今、あなたは「MessageProducer」、「set up、let's update our」、「UserService」を使用してください。

「Java
@サービス
パブリッククラスUserService {

    // ...他のコード

    @Autowired
    private MessageProducer messageProducer;

    公開ユーザーcreateUser（ユーザーユーザー）{
        User savedUser = userRepository.save（ユーザー）;
        messageProducer.sendMessage("ユーザートピック", savedUser.toString());
        保存されたユーザーを返します。
    }

    // ...他のコード
}
```

私はあなたに言うと、私は「ユーザー」のメソッドを使って「UserService」を使ってメッセージを送ります。

今、私たちはシンプルな ```MessageListener ''を作ります。

「Java
@要素
パブリック クラス MessageListener {

    @Autowired
    プライベートUserDtoService userDtoService;

    @KafkaListener（トピック=「ユーザートピック」）
    パブリック無効handleMessage（文字列メッセージ）{
        //メッセージを逆シリアル化
        // UserDto エンティティの作成または更新
        // UserDto エンティティの保存
    }
}
```

私はあなたが言う、私はあなたのメッセージ「メッセージリスト」を使って「@KafkaListener」を使っているので、私はカフカのトピックを使います。 We've also added a ``handleMessage()```method that deserializes the message, creates or updates the ``UserDto```entity, and saves the ``UserDto```entity.

今、私たちのアップデートは「MessageListener」を使用して「MessageListener」を使用します。

「Java
@RestController
@RequestMapping("/ユーザー")
パブリッククラスUserController {

    // ...他のコード

    @Autowired
    プライベート MessageListener messageListener;

    // ...他のコード
}
```

私はそれを言う、私はadded a「messageListener」、「field to our」、「UserController」です。 This will allow us to consume messages from our Kafka topic and update the read model accordingly.

### Use an Event Sourcing Pattern

Another best practice for using CQRS in a Spring Boot application is to use an event sourcing pattern. Event sourcing is a pattern for persisting entities as a series of events.

The benefits of using event sourcing include improved scalability, performance, and maintainability. Event sourcing can also make it easier to track changes to the data model over time.

In this example, we'll use the Axon Framework, which is a popular framework for implementing the event sourcing pattern.

First、we'll add the following dependencies to our ```pom.xml ```file：

```xml
<依存性>
    <groupId>org.axonframework</groupId>
    <artifactId>axon-spring-boot-starter</artifactId>
    <バージョン>${axon.version}</バージョン>
</依存性>
```

次へ、私たちは単純な「ユーザー」を手に入れることができます。

「Java
@要素
パブリッククラスUserEventHandler {

    @Autowired
    プライベートUserDtoRepository userDtoRepository;

    @イベントハンドラ
    公開無効 on(UserCreatedEvent イベント) {
        UserDto userDto = new UserDto();
        userDto.setId(event.getId());
        userDto.setFirstName(event.getFirstName());
        userDto.setLastName(event.getLastName());
        userDtoRepository.save（userDto）;
    }

    @イベントハンドラ
    公開無効 on(UserUpdatedEvent イベント) {
        UserDto userDto = userDtoRepository.findById(event.getId()).orElse(null);
        if(userDto == null) {
            返品
        }
        userDto.setFirstName(event.getFirstName());
        userDto.setLastName(event.getLastName());
        userDtoRepository.save（userDto）;
    }

    @イベントハンドラ
    公開無効 on(UserDeletedEvent イベント) {
        UserDto userDto = userDtoRepository.findById(event.getId()).orElse(null);
        if(userDto == null) {
            返品
        }
        userDtoRepository.delete(userDto);
    }
}
```

私はあなたを言う、私はあなたの「ユーザー」と「@EventHandler」を使って言うことができます。 We've also added ```on () '' methods for handling the ```UserCreatedEvent ''、 ```UserUpdatedEvent ''、および ```UserDeletedEvent '' events。 These methods will create, update, and delete ```UserDto ```' entities, respectively.

今、私たちのアップデートはあなたの「UserEventHandler」の「あなたのユーザーUserHandler」です。

「Java
@サービス
パブリッククラスUserService {

    // ...他のコード

    @Autowired
    プライベートEventBus eventBus;

    公開ユーザーcreateUser（ユーザーユーザー）{
        // ...他のコード
        eventBus.publish(new UserCreatedEvent(user.getId(), user.getFirstName(), user.getLastName()));
        返品ユーザー
    }

    公開ユーザー updateUser (ユーザーユーザー) {
        // ...他のコード
        eventBus.publish(new UserUpdatedEvent(user.getId(), user.getFirstName(), user.getLastName()));
        返品ユーザー
    }

    パブリック無効 deleteUser (ユーザー ユーザー) {
        // ...他のコード
        eventBus.publish(new UserDeletedEvent(user.getId()));
    }
}
```

私はあなたに言う、私はあなたの「UserService」、「field to our」、「UserService」を追加しました。 This field will be used to publish events related to our ```User '' entity. We've also added ```publish（） '' methods for publishing the ```UserCreatedEvent ''、 ```UserUpdatedEvent ''、そして ' These methods will be called when a ``User'' ' entity is created, updated, or deleted, respectively.

今、私たちのアップデートはあなたの「UserEventHandler」の「あなたのユーザーUserHandler」です。

「Java
@RestController
@RequestMapping("/ユーザー")
パブリッククラスUserController {

    // ...他のコード

    @Autowired
    プライベートUserEventHandler userEventHandler;

    // ...他のコード
}
```

私はそれを言う、私はadded a「UserController」に「userEventHandler」フィールドを追加しました。これにより、「EventBus」でイベントを消費し、それに応じて読み取りモデルを更新できます。

##結論

この記事では、Spring BootアプリケーションでCQRSパターンを実装する方法について説明しました。 Spring BootアプリケーションでCQRSを使用するためのいくつかのベストプラクティスも確認しました。