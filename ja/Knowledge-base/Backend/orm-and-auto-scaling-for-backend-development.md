---
title: バックエンド開発のための ORM と自動スケーリング
description: 
published: true
date: 2023-02-17T18:04:23.444Z
tags: 
editor: markdown
dateCreated: 2023-01-30T12:17:11.427Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [ORM and Auto-scaling for Backend Development***English** version of this document is available*](/en/Knowledge-base/Backend/orm-and-auto-scaling-for-backend-development)
{.links-list}
 


#バックエンド開発のためのORMとAuto-Scaling

この記事では、バックエンド開発のための2つの重要な概念、ORM（Object Relational Mapping）と自動サイジングについて説明します。

## ORM

ORMは、開発者がオブジェクトを使用してデータベースを操作できるようにする技術です。つまり、オブジェクトとデータベーステーブル間のマッピングを提供します。このマッピングは2つの方法で行うことができます。

- **コメントベースのマッピング**：このアプローチでは、開発者はクラスとデータベーステーブル間のマッピングを指定するメタデータとしてJavaクラスにコメントを追加します。

- **XMLベースのマッピング**：このアプローチでは、開発者はXMLドキュメントへのマッピングを指定します。このドキュメントは、ORMツールでデータベーススキーマとJavaクラスを生成するために使用されます。

ORMを使用すると、次のような利点がいくつかあります。

- **開発がより迅速で簡単になります**：開発者はアプリケーションのビジネスロジックに集中し、ORMツールにデータベースの対話を処理させることができます。

- **作成する必要があるコードの量を減らす**：ORMツールはデータベース対話のためのSQLコードを生成できるため、開発者は直接このコードを書く必要はありません。

- **アプリケーションの移植性を高める**：データベースの相互作用はORMツールによって処理されるため、必要に応じてアプリケーションを別のデータベースに簡単に移行できます。

Hibernate、EclipseLink、iBatisなどの複数のORMツールを使用できます。この記事では、Hibernateに焦点を当てます。

### 休止状態

Hibernateは、注釈ベースとXMLベースのマッピングの両方を提供する広く使用されているORMツールです。また、キャッシュおよび遅延ローディングのサポートなど、さまざまな機能があります。

 Hibernateを使用してJavaクラスをデータベーステーブルにマッピングする方法を見てみましょう。次のJavaクラスを例として使用します。

```java
public class Employee {
    private Long id;
    private String name;
    private Integer age;
    private Double salary;
    
    // Getters and setters...
}
```

そしてそれを次のデータベーステーブルにマップします。

```sql
CREATE TABLE employee(
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    名前 TEXT,
    age INTEGER,
    salary REAL
）;
```

マッピングは2つの方法で行うことができます。

- **コメントベースのマッピング**：

  ```java
  @Entity
  @Table(name="employee")
  public class Employee {
      @Id
      @Column(name="id")
      private Long id;
  
      @Column(name="name")
      private String name;
  
      @Column(name="age")
      private Integer age;
  
      @Column(name="salary")
      private Double salary;
  
      // Getters and setters...
  }
  ```

- **XMLベースのマッピング**：

  ```xml
  <hibernate-mapping>
      <class name="Employee" table="employee">
          <id name="id" column="id">
              <generator class="native"/>
          </id>
          <property name="name" column="name"/>
          <property name="age" column="age"/>
          <property name="salary" column="salary"/>
      </class>
  </hibernate-mapping>
  ```

どちらの場合も、Employeeクラスがマップされるデータベース表の名前を指定する必要があります。さらに、Employeeクラスの各フィールドのマッピングを指定する必要があります。 idフィールドには、テーブルの主キーであり、データベースによって生成される（自動インクリメント）を指定する必要があります。

マッピングが完了したら、従業員を挿入、更新、削除、および照会するコードを作成できます。

```java
// Insert an employee
Employee emp = new Employee();
emp.setName("John Smith");
emp.setAge（30）;
emp.setSalary（45000.0）;

Session session = sessionFactory.openSession();
session.beginTransaction();

session.save(emp);

session.getTransaction().commit();
session.close();

// Update an employee
emp.setSalary（50000.0）;

session = sessionFactory.openSession();
session.beginTransaction();

session.update(emp);

session.getTransaction().commit();
session.close();

// Delete an employee
session = sessionFactory.openSession();
session.beginTransaction();

session.delete(emp);

session.getTransaction().commit();
session.close();

// Query employees
List<Employee> employees = session.createQuery("from Employee").list();

for (Employee e: employees) {
    System.out.println(e.getName() + " " + e.getAge() + " " + e.getSalary());
}
```

上記のコードスニペットでは、まず従業員をデータベースに挿入します。その後、従業員の給与を更新し、最後に従業員を削除します。また、データベースを照会してすべての従業員のリストを取得します。

##自動サイズ変更

自動拡張は、開発者がアプリケーションを水平に拡張できるようにする技術です。つまり、開発者はアプリケーションへの負荷が増加したときにアプリケーションに新しいサーバーを追加できます。これは、単一サーバーのリソースを増やす垂直方向の拡張とは対照的です。

自動サイズ変更を使用すると、2つの利点があります。

- **アプリケーションはより多くの負荷を処理できます**：必要に応じて新しいサーバーを追加できるため、アプリケーションはパフォーマンスの問題なしにより多くのトラフィックを処理できます。

- **より費用対効果が高い**：必要に応じて新しいサーバーを追加および削除できるため、開発者は使用したリソースに対してのみ支払います。

自動サイズ変更は手動または自動で行うことができます。この記事では、自動自動サイジングに焦点を当てます。

###自動自動サイズ変更

自動自動サイジングには、ツールを使用してアプリケーションの負荷を監視し、必要に応じてサーバーを追加および削除することが含まれます。 Apache httpd、nginx、HAProxyなど、いくつかのツールを使用できます。この記事では、Apache httpdに焦点を当てます。

Apache httpdは、自動サイジングアプリケーションの作成に使用できる広く使用されているWebサーバーです。必要に応じてサーバーを追加および削除するために使用できるmod_clusterというモジュールがあります。

mod_cluster モジュールは次のように動作します。

- **アプリケーションの負荷を監視します**：モジュールは定期的にアプリケーションに要求を送信し、応答時間を確認します。応答時間が長すぎると、アプリケーションに過負荷がかかり、新しいサーバーを追加する必要があります。

- **必要に応じてサーバーを追加および削除します**：モジュールはmod_cluster管理インターフェースに要求して、アプリケーションに新しいサーバーを追加できます。同様に、不要になったサーバーを削除できます。

mod_clusterモジュールを使用して自動拡張アプリケーションを作成する方法を見てみましょう。次のApache httpd設定を使用します。

「apache
<VirtualHost *:80>
    ServerName www.example.com
    
    <Directory /var/www/html>
        Require all granted
    </Directory>
    
    <Location /cluster-manager>
        SetHandler cluster-manager
    </Location>
    
    <Proxy balancer://mycluster>
        BalancerMember http://localhost:8000
        BalancerMember http://localhost:8001
    </Proxy>
    
    <Proxy*>
        Order deny,allow
        Allow from all
    </Proxy>
    
    ProxyPass / balancer://mycluster/
    ProxyPassReverse / balancer://mycluster/
</VirtualHost>
```

上記の構成では、www.example.comドメインへの要求を処理する仮想ホストを定義しました。また、2つのサーバー（localhost：8000とlocalhost：8001）を含むプロキシバランサーも定義しました。最後に、必要に応じてサーバーを追加および削除するようにmod_clusterを設定しました。

それでは、Apache httpdサーバーが提供する簡単なPHPアプリケーションを作成しましょう。

```php
<?php
$server = $_SERVER['SERVER_ADDR'];
echo "Hello, World! I'm running on $server";
?>
```

そして我々はそれを2つのサーバーで実行します：

- ローカルホスト：8000
- ローカルホスト：8001

ユーザーがwww.example.com Webサイトにアクセスすると、次のページが表示されます。

```
Hello, World! I'm running on 127.0.0.1
```

より多くの要求を作成してアプリケーションの負荷を増やすと、mod_clusterは必要に応じて新しいサーバーを追加します。たとえば、1秒あたり10個の要求を作成すると、mod_clusterは2つの新しいサーバーを追加します。

##結論

この記事では、バックエンド開発のための2つの重要な概念、ORMと自動サイジングについて説明しました。 ORMを使用してJavaクラスをデータベーステーブルにマップする方法と、自動拡張機能を使用して、必要に応じてアプリケーションに新しいサーバーを追加する方法について説明しました。