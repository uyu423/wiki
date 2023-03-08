---
title: MySQL 06: SQL에서 데이터 조작: INSERT, UPDATE, DELETE 및 ALTER
description: 
published: true
date: 2023-02-06T12:32:55.344Z
tags: 
editor: markdown
dateCreated: 2023-02-06T12:32:53.731Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [MySQL 06: Data manipulation in SQL: INSERT, UPDATE, DELETE, and ALTER***English** document is available*](/en/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-06-data-manipulation-in-sql-insert-update-delete-and-alter)
{.links-list}


MySQL 06: SQL에서 데이터 조작: INSERT, UPDATE, DELETE 및 ALTER
==================================================== ==========

이 게시물에서는 INSERT, UPDATE, DELETE 및 ALTER 문을 사용하여 SQL에서 데이터 조작을 다룰 것입니다.

### 삽입

INSERT 문은 데이터베이스 테이블에 데이터를 삽입하는 데 사용됩니다. INSERT 구문은 다음과 같습니다.

```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```

여기서 ```table_name```은 데이터를 삽입하려는 테이블의 이름이고 ```(column1, column2, column3, ...)```은 삽입할 열의 목록입니다. 데이터를 삽입하고 싶습니다. ```VALUES (value1, value2, value3, ...)```는 삽입하려는 값의 목록입니다.

테이블의 모든 열에 대해 값을 지정할 필요는 없습니다. 열 값을 지정하지 않으면 해당 열의 기본값이 사용됩니다.

다음은 테이블에 데이터를 삽입하는 예입니다.

```sql
INSERT INTO products (name, price)
VALUES ('Widget', 9.99);
```

이것은 이름이 ```Widget```이고 가격이 ```9.99```인 ```products``` 테이블에 행을 삽입합니다.

한 번에 테이블에 여러 행을 삽입할 수도 있습니다.

```sql
INSERT INTO products (name, price)
VALUES ('Widget', 9.99),
       ('Gadget', 19.99),
       ('Doohickey', 29.99);
```

그러면 ```products``` 테이블에 세 개의 행이 삽입됩니다.

### 업데이트

UPDATE 문은 데이터베이스 테이블의 데이터를 업데이트하는 데 사용됩니다. UPDATE 구문은 다음과 같습니다.

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, column3 = value3, ...
WHERE condition;
```

여기서 ```table_name```은 업데이트하려는 테이블의 이름이고, ```SET column1 = value1, column2 = value2, column3 = value3, ...```는 원하는 열의 목록입니다. 업데이트할 열의 새 값과 ```WHERE 조건```은 업데이트할 행을 지정하는 조건입니다.

예를 들어 다음 명령문은 ```name```이 ```Widget```인 ```products``` 테이블의 모든 행에 대해 ```price``` 열을 업데이트합니다.

```sql
UPDATE products
SET price = 11.99
WHERE name = 'Widget';
```

한 번에 여러 열을 업데이트할 수도 있습니다.

```sql
UPDATE products
SET price = 11.99,
    name = 'NewWidget'
WHERE name = 'Widget';
```

### 삭제

DELETE 문은 데이터베이스 테이블에서 데이터를 삭제하는 데 사용됩니다. DELETE 구문은 다음과 같습니다.

```sql
DELETE FROM table_name
WHERE condition;
```

여기서 ```table_name```은 데이터를 삭제할 테이블의 이름이고 ```WHERE condition```은 삭제할 행을 지정하는 조건입니다.

예를 들어, 다음 명령문은 ```name```이 ```Widget```인 ```products``` 테이블에서 모든 행을 삭제합니다.

```sql
DELETE FROM products
WHERE name = 'Widget';
```

### 변경

ALTER 문은 데이터베이스 테이블의 구조를 수정하는 데 사용됩니다. ALTER 구문은 다음과 같습니다.

```sql
ALTER TABLE table_name
ADD column_name data_type;

ALTER TABLE table_name
MODIFY column_name data_type;

ALTER TABLE table_name
DROP column_name;
```

여기서 ```table_name```은 수정하려는 테이블의 이름이고 ```ADD column_name data_type```은 지정된 데이터 유형 ```MODIFY column_name data_type``을 사용하여 테이블에 새 열을 추가합니다. `는 기존 컬럼의 데이터 타입을 변경하고, ```DROP column_name```은 테이블에서 컬럼을 삭제합니다.

예를 들어 다음 명령문은 ```products``` 테이블에 새로운 ```price``` 열을 추가합니다.

```sql
ALTER TABLE products
ADD price decimal(5,2);
```

다음 명령문은 ```price``` 열의 데이터 유형을 ```integer```로 변경합니다.

```sql
ALTER TABLE products
MODIFY price integer;
```

추가 정보
----------------------

다음은 SQL에서 데이터 조작 작업을 할 때 유의해야 할 몇 가지 추가 사항입니다.

* ```AUTO_INCREMENT``` 열이 있는 테이블에 데이터를 삽입하는 경우 해당 열에 ```NULL``` 값을 지정하면 MySQL이 자동으로 새 값을 생성합니다.

* 데이터를 업데이트하거나 삭제하는 경우 ```WHERE``` 절은 선택 사항입니다. ```WHERE``` 절을 생략하면 테이블의 모든 행이 업데이트되거나 삭제됩니다.

* ```UPDATE``` 및 ```DELETE``` 문과 함께 ```ORDER BY``` 및 ```LIMIT``` 절을 사용하여 업데이트 또는 삭제할 행을 지정할 수 있습니다.

* ```ALTER TABLE``` 문을 사용하여 테이블의 열을 추가, 수정 또는 삭제할 수 있으며 인덱스를 추가하거나 삭제할 수 있습니다.

* ```ALTER TABLE``` 문을 사용하여 테이블의 이름을 변경할 수 있습니다.

외부 자원
------------------

다음은 SQL에서 데이터 조작에 대해 자세히 읽을 수 있는 몇 가지 외부 리소스입니다.

* [MySQL 튜토리얼](https://dev.mysql.com/doc/refman/5.7/en/sql-tutorial.html)
* [SQL INSERT 문](https://www.w3schools.com/sql/sql_insert.asp)
* [SQL UPDATE 문](https://www.w3schools.com/sql/sql_update.asp)
* [SQL DELETE 문](https://www.w3schools.com/sql/sql_delete.asp)
* [SQL ALTER TABLE 문](https://www.w3schools.com/sql/sql_alter.asp)