# Database

> 체계화된 데이터의 모임
>
> 각 자료의 중복을 없애고 구조화하여 기억하는 집합체





#### 장점

- 데이터 중복 최소화
- 데이터 무결성
- 데이터 일관성
- 데이터 독립성
- 데이터 표준화
- 데이터 보안 유지





---





# RDB

> key와 value가 연결된 관계를 표로 정리한 데이터베이스





#### RDBMS

>  RDB를 기반으로 하는 데이터베이스 관리시스템

- MySQL
- SQLite
- PostgreSQL
- ORACLE
- MS SQL





---





# SQL

> **S**tructured **Q**uery **L**anguage
>
> RDBMS의 데이터 관리를 위한 언어





#### 분류

- DDL : 데이터 정의 언어
  - CREATE
  - DROP
  - ALTER
- DML : 데이터 조작 언어
  - INSERT
  - SELECT
  - UPDATE
  - DELETE
- DCL : 데이터 제어 언어
  - GRANT
  - REVOKE
  - COMMIT
  - ROLLBACK





### 데이터베이스 생성 및 삭제

```bash
# sqlite 실행
$ sqlite3 tutorial.sqlite3
```

```sqlite
-- 데이터베이스 생성
-- .은 sqlite의 기능을 의미
.database

-- 데이터 출력 결과의 표시형태를 지정
.mode csv

-- hellodb.csv 파일 examples라는 테이블에 가져오기
.import hellodb.csv examples

-- 데이터베이스에 작성된 테이블 확인
.tables

-- examples 테이블의 스키마 조회
.schema examples

-- examples 테이블의 전체 레코드 조회
SELECT * FROM examples;

-- 출력결과에 column 이름 붙이기
.headers on

-- 행과 열의 형태로 출력하기
.mode column
```





> 확장프로그램을 이용하여 파일에 SQL 명령어를 작성하고 변경사항 확인 가능
>
> sqlite 파일 - Open Database - SQLITE EXPLORER - New Query 

```sql
-- 테이블 생성 각 칼럼명, 타입 지정 
CREATE TABLE classmates(
id INTEGER PRIMARY KEY,
name TEXT
);

-- classmates 테이블 삭제
DROP TABLE classmates;

-- classmates 테이블 재생성
-- 따로 PRIMARY KEY를 지정해주지 않으면, SQLite는 자동으로 rowid 컬럼을 정의
CREATE TABLE classmates(
name TEXT,
age INT,
address TEXT
);

-- 특정 열에 특정 데이터 삽입
INSERT INTO classmates (name, age) VALUES ('홍길동', 23);

-- 모든 열에 데이터를 삽입한다면 column을 명시하지 않아도 됨
INSERT INTO classmates VALUES ('홍길동', 30, '서울');

-- classmates 테이블 삭제
DROP TABLE classmates;

-- classmates 테이블 재생성
-- NOT NULL을 이용해 값을 비우지 못하도록 설정
CREATE TABLE classmates(
name TEXT NOT NULL,
age INT NOT NULL,
address TEXT NOT NULL
);

-- 여러 데이터를 한번에 삽입
INSERT INTO classmates VALUES 
('홍길동', 30, '서울'),
('김철수', 30, '대전'),
('이싸피', 26, '광주'),
('박삼성', 29, '구미'),
('최전자', 28, '부산');
```





### 조회

```sql
-- classmates의 rowid, name 칼럼 조회 
SELECT rowid, name FROM classmates;

-- 데이터를 원하는 수만큼 조회하기
SELECT rowid, name FROM classmates LIMIT 1;

-- 세번째 데이터 조회하기
-- OFFSET만큼 공백을 두고 데이터를 꺼내옴
SELECT rowid, name FROM classmates LIMIT 1 OFFSET 2;

-- address가 서울인 데이터 조회하기
SELECT rowid, name FROM classmates WHERE address='서울';

-- 전체 age를 중복없이 조회하기
SELECT DISTINCT age FROM classmates;
```





### 삭제

> 중복되지 않는 값인 primary key나 rowid를 이용해 삭제하자

```sql
DELETE FROM classmates WHERE rowid=5;

-- SQLite는 기본적으로 삭제된 id를 재사용
-- AUTOCREMENT를 통해 설정 가능 (django에서는 기본값으로 사용)
CREATE TABLE new_table_name(
id INTEGER PRIMARY KEY AUTOINCREMENT,
...
);
```





### 수정

> 마찬가지로, 중복되지 않는 값인 primary key나 rowid를 이용해 삭제하자

```sql
UPDATE classmates SET name='홍길동', address='제주도' WHERE rowid=5;
```





### Aggregate function

> 집계함수
>
> 데이터 집합에 대해 계산을 수행해 단일 값을 반환
>
> SELECT 구문에서만 사용됨

#### 종류

- COUNT

- AVG

- MAX

- MIN

- SUM

```sqlite
-- user 테이블을 만들어 csv 파일 불러오기
CREATE TABLE users (
first_name TEXT NOT NULL,
last_name TEXT NOT NULL,
age INTEGER NOT NULL,
country TEXT NOT NULL,
phone TEXT NOT NULL,
balance INTEGER NOT NULL,
);

.mode csv
.import users.csv users
.tables
```

```sql
-- users의 레코드 수 조회
SELECT COUNT(*) FROM users;
-- 집계된 결과의 컬럼명을 바꿔서 조회할 수 있음
SELECT COUNT(*) AS cnt FROM users;

-- 30살 이상인 사람들의 평균 나이
SELECT AVG(age) FROM users WHERE age>=30;
-- 가장 어린 나이
SELECT MIN(age) FROM users
-- 잔액이 가장 높은 사람과 그 액수
SELECT first_name, MAX(balance) FROM users
-- 30살 이상인 사람의 잔액 합계
SELECT SUM(balance) FROM users WHERE age>=30;
```





### LIKE operator

> 패턴을 기반으로 데이터를 조회
>
> wildcards를 이용해 패턴을 구성

#### wildcards : 알 수 없는 값

- `%` : 임의의 0개 이상의 문자열
- `_` : 임의의 단일 문자

```sql
-- 나이가 20대인 사람 조회
SELECT * FROM users WHERE age LIKE '2_';
-- 전화번호가 02로 시작하는 사람 조회
SELECT * FROM users WHERE phone LIKE '02-%';
-- 이름이 준으로 끝나는 사람 조회
SELECT * FROM users WHERE first_name LIKE '%준';
```





### ORDER BY

> 조회 결과 집합을 정렬
>
> 오름차순(ASC, Default), 내림차순(DESC) 제공

```sql
-- 나이 오름차순 상위 10개 조회
SELECT * FROM users ORDER BY age ASC LIMIT 10;

-- 나이, 성을 기준으로 오름차순 상위 10개 조회
-- 나이로 먼저 정렬한 후 같은 나이 내에서 성 기준 정렬
SELECT * FROM users ORDER BY age, last_name ASC LIMIT 10;
```





### GROUP BY

> 데이터를 특정 기준으로 종합
>
> WHERE절과 함께 사용하는 경우 반드시 WHERE절 뒤에 작성

```sql
-- 성씨마다 몇명씩 있는지 조회
SELECT lasr_name, COUNT(*) FROM users GROUP BY last_name;
```





### AlTER TABLE

> 테이블명, 컬럼 추가, 컬럼명 변경 등 테이블의 구조를 변경
>
> 컬럼명 변경은 SQLite 3.25.0 부터 제공하는 기능

```sql
-- 테이블 생성
CREATE TABLE articles (
title TEXT NOT NULL,
content TEXT NOT NULL
);

-- 테이블명 변경
ALTER TABLE articles RENAME TO news;

-- 컬럼 추가
ALTER TABLE news ADD COLUMN created_at TEXT
-- NOT NULL 속성의 컬럼을 추가할 때는, 반드시 디폴트값 지정해야함
ALTER TABLE news ADD COLUMN created_at TEXT NOT NULL DEFAULT '디폴트';
```
