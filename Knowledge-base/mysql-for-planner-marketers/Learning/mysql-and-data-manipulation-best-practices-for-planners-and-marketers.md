---
title: MySQL 및 데이터 조작: 기획자와 마케터를 위한 모범 사례
description: 
published: true
date: 2023-02-06T19:33:04.473Z
tags: 
editor: markdown
dateCreated: 2023-02-06T19:32:58.754Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [MySQL and Data Manipulation: Best Practices for Planners and Marketers***English** document is available*](/en/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-and-data-manipulation-best-practices-for-planners-and-marketers)
{.links-list}


## MySQL 및 데이터 조작: 기획자와 마케터를 위한 모범 사례

데이터 조작은 마케팅 목적이든 계획 목적이든 관계없이 데이터로 작업하는 모든 사람에게 중요한 기술입니다. MySQL은 사용자가 다양한 방법으로 데이터를 조작할 수 있도록 하는 널리 사용되는 데이터베이스 관리 시스템입니다.

이 게시물에서는 MySQL 및 데이터 조작 작업에 대한 몇 가지 모범 사례를 다룰 것입니다. 추가 학습을 위한 몇 가지 팁과 리소스도 제공합니다.

### MySQL 시작하기

MySQL을 처음 사용하는 경우 공식 [MySQL 설명서](https://dev.mysql.com/doc/)부터 시작하는 것이 좋습니다. 이 리소스는 설치에서 데이터베이스 및 테이블 작업에 이르기까지 모든 것을 다룹니다.

MySQL의 기본 사항에 익숙해지면 데이터 작업을 시작할 수 있습니다. 이를 수행하는 방법에는 몇 가지가 있지만 가장 일반적인 두 가지인 `SELECT` 및 `INSERT` 문에 중점을 둘 것입니다.

#### `SELECT` 문

`SELECT` 문은 데이터베이스에서 데이터를 쿼리하는 데 사용됩니다. 예를 들어 다음 쿼리는 `users`라는 테이블에서 모든 행을 선택합니다.

```sql
SELECT * FROM users;
```

`SELECT` 문을 사용하여 테이블에서 특정 열을 선택할 수도 있습니다. 예를 들어 다음 쿼리는 `users` 테이블에서 `id` 및 `name` 열을 선택합니다.

```sql
SELECT id, name FROM users;
```

'SELECT' 문은 'WHERE' 절과 함께 사용하여 특정 기준을 충족하는 행을 선택할 수도 있습니다. 예를 들어 다음 쿼리는 `id`가 10보다 큰 `users` 테이블에서 모든 행을 선택합니다.

```sql
SELECT * FROM users WHERE id > 10;
```

[MySQL 설명서](https://dev.mysql.com/doc/refman/8.0/en/select.html)에서 알아볼 수 있는 `SELECT` 문을 사용하는 다른 많은 방법이 있습니다.

#### `INSERT` 문

'INSERT' 문은 데이터베이스에 데이터를 삽입하는 데 사용됩니다. 예를 들어 다음 쿼리는 `users` 테이블에 새 행을 삽입합니다.

```sql
INSERT INTO users (id, name) VALUES (1, 'John Doe');
```

'INSERT' 문은 'UPDATE' 및 'DELETE' 절과 함께 사용되어 데이터베이스의 데이터를 업데이트하거나 삭제할 수도 있습니다. 예를 들어 다음 쿼리는 `users` 테이블에서 `id`가 1인 행의 `name` 열을 업데이트합니다.

```sql
UPDATE users SET name = 'John Smith' WHERE id = 1;
```

다음 쿼리는 `users` 테이블에서 `id`가 1인 행을 삭제합니다.

```sql
DELETE FROM users WHERE id = 1;
```

[MySQL 설명서](https://dev.mysql.com/doc/refman/8.0/ ko/insert.html).

### MySQL 및 데이터 조작을 위한 모범 사례

이제 MySQL 및 데이터 조작의 기본 사항에 익숙해졌으므로 몇 가지 모범 사례를 살펴보겠습니다.

#### 데이터 백업

가장 중요한 모범 사례 중 하나는 항상 데이터를 백업하는 것입니다. 이렇게 하면 문제가 발생한 경우 백업에서 데이터를 복원할 수 있습니다.

데이터를 백업하는 방법에는 몇 가지가 있지만 `mysqldump` 유틸리티를 사용하는 것이 좋습니다. 이 유틸리티를 사용하여 SQL 형식으로 데이터베이스 백업을 생성할 수 있습니다. 예를 들어 다음 명령은 `users` 데이터베이스의 백업을 만듭니다.

```
mysqldump -u root -p users > users.sql
```

`root`를 MySQL 사용자 이름으로 바꾸고 `user`를 데이터베이스 이름으로 바꿉니다. 또한 MySQL 암호를 입력하라는 메시지가 표시됩니다.

#### 데이터에 자리 표시자 사용

데이터베이스에 데이터를 삽입할 때 데이터에 자리 표시자를 사용하는 것이 중요합니다. 이는 SQL 삽입 공격을 방지하는 데 도움이 됩니다.

예를 들어 다음 `INSERT` 문을 고려하십시오.

```sql
INSERT INTO users (id, name) VALUES (1, 'John Doe');
```

이 문에서 `id` 및 `name` 열은 하드 코딩되어 있습니다. 이것은 SQL 인젝션 공격에 대한 문을 열어두기 때문에 좋은 습관이 아닙니다.

대신 데이터에 자리 표시자를 사용해야 합니다. 예를 들어:

```sql
INSERT INTO users (id, name) VALUES (?, ?);
```

이 문에서 `id` 및 `name` 열은 `?` 자리 표시자로 대체됩니다. 문을 실행할 때 이러한 자리 표시자에 대한 값을 제공합니다.

#### 적절한 데이터 유형 사용

데이터베이스를 생성할 때 데이터에 적절한 데이터 유형을 사용하는 것이 중요합니다. 예를 들어 날짜를 저장하는 경우 `DATE` 데이터 유형을 사용해야 합니다. 숫자를 저장하는 경우 `INT` 데이터 유형을 사용해야 합니다.

잘못된 데이터 유형을 사용하면 오류 및 예기치 않은 결과가 발생할 수 있습니다. 예를 들어 `INT` 열에 날짜를 저장하려고 하면 오류가 발생합니다.

#### 와일드카드 사용 금지

`SELECT` 문을 사용할 때 와일드카드(`*`)를 사용하지 않는 것이 중요합니다. 이는 와일드카드가 많은 양의 데이터를 반환하여 데이터베이스 속도를 저하시킬 수 있기 때문입니다.

와일드카드를 사용하는 대신 반환하려는 특정 열을 지정해야 합니다. 예를 들어:

```sql
SELECT id, name FROM users;
```

이 문에서는 `id` 및 `name` 열만 반환됩니다.

#### 인덱스 사용

대규모 데이터베이스로 작업할 때는 인덱스를 사용하는 것이 중요합니다. 인덱스는 특정 데이터에 대한 빠른 액세스를 허용하여 데이터베이스 성능을 향상시키는 데 도움이 됩니다.

예를 들어 백만 개의 행이 있는 테이블이 있고 `id`가 10,000보다 큰 모든 행을 선택하려는 경우 인덱스를 사용하여 이러한 행을 빠르게 찾을 수 있습니다. 인덱스가 없으면 데이터베이스는 일치하는 행을 찾기 위해 전체 테이블을 검색해야 하므로 시간이 오래 걸립니다.

색인을 생성하려면 `CREATE INDEX` 문을 사용할 수 있습니다. 예를 들어 다음 명령문은 `users` 테이블의 `id` 열에 인덱스를 생성합니다.

```sql
CREATE INDEX idx_users_id ON users (id);
```

#### 불필요한 데이터 조작 방지

데이터로 작업할 때 불필요한 데이터 조작을 피하는 것이 중요합니다. 이로 인해 오류가 발생하고 성능이 저하될 수 있습니다.

예를 들어 다음 `UPDATE` 문을 고려하십시오.

```sql
UPDATE users SET name = 'John Doe' WHERE id = 1;
```

이 문에서 `id`가 1인 행에 대해 `name` 열이 업데이트됩니다. 그러나 `name` 열이 이미 `John Doe`인 경우 이 `UPDATE` 문은 필요하지 않습니다.

`이름` 열을 업데이트하는 대신 먼저 업데이트가 필요한지 확인할 수 있습니다. 예를 들어:

```sql
SELECT name FROM users WHERE id = 1;
```

`name` 열이 이미 `John Doe`인 경우 `UPDATE` 문을 건너뛸 수 있습니다.

### 추가 정보

#### 경고

- 데이터를 조작하기 전에 항상 데이터를 백업하십시오.
- 데이터 조작 시 주의하십시오. 잘못된 데이터 조작은 데이터 손실로 이어질 수 있습니다.

#### 위험

- 대규모 데이터베이스로 작업할 때 와일드카드를 사용하지 마십시오. 이로 인해 데이터베이스 속도가 느려질 수 있습니다.
- 데이터를 불필요하게 조작하지 마십시오. 이로 인해 오류가 발생하고 성능이 저하될 수 있습니다.

### 추가 학습을 위한 리소스

- [MySQL 문서](https://dev.mysql.com/doc/)
- [MySQL을 이용한 데이터 조작](https://www.digitalocean.com/community/tutorials/how-to-manipulate-data-with-mysql)
- [MySQL 모범 사례](https://www.a2hosting.com/kb/developer-corner/mysql/mysql-best-practices)