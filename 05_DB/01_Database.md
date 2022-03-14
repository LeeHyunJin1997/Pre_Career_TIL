# Database

- 체계화된 데이터의 모임
- 자료의 중복을 없애고 구조화



# 관계형 데이터베이스

- Relational Database
- 키와 값의 관계를 표로 정리한 데이터베이스
- 스키마 (schema) : 데이터베이스의 전반적인 명세
- 테이블 (table) : 행과 열로 이루어진 데이터 요소들의 집합
  - 열 (column) : 고유한 데이터 형식
  - 행(row) : 실제 데이터
- 기본키 (Primary Key) : 각 행의 고유값



# 관계형 데이터베이스 관리 시스템

- Relational Database Management System

- 권장하는 데이터 타입
  - INTEGER
  - TEXT
  - BLOB
  - REAL
  - NUMERIC



# SQL

- Structured Query Language
- RDBMS에서 사용하는 프로그래밍 언어
- 데이터베이스 스키마 생성 및 수정, 자료 검색 관리
- 분류
  - DDL : 데이터 정의
  - DML : 데이터 조작
  - DCL : 데이터 제어 



# CRUD

- CREATE

  - INSERT

    ```sql
    INSERT INTO table_name (column1, column2) VALUES (value1, value2)
    ```

  -  

-  READ

  -  SELECT
  -  
  - 