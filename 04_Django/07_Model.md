# Model

- Django는 model을 통해 데이터에 접속하고 관리
- 각각의 model은 하나의 데이터베이스 테이블에 매핑



# DB 용어

- 데이터베이스 (DB)

  - 체계화된 데이터의 모임

- 쿼리 (Query)

  - 데이터베이스를 조작하기 위한 명령어
  - 쿼리를 날리다 = 데이터베이스를 조작하다

- 스키마 (Schema)

  - 데이터베이스의 자료 구조, 표현, 관계 등을 정의

  - 테이블의 형태를 간단히 나타낸 것

- 테이블 (Table)

  - 열(column)
  - 행(row)
  - **P**rimary **K**ey :각 행(레코드)의 고유값

- 필드 (Field)

  - 각 컬럼(column)의 타입



# ORM

- **O**bject-**R**elational-**M**apping
- 시스템 (Django-SQL) 간의 데이터를 변환
- Django는 내장 Django ORM을 사용
- 빠른 웹개발에 중점을 둔 현대 웹 프레임워크
- 장점
  - SQL를 잘 알지 못해도 DB 조작 가능
- 단점
  - ORM만으로 완전한 SQL 기능을 구현하기 어려움
  - 효율성이 다소 떨어짐



# Model 생성

```python
# app/models.py

# 각 모델은 django.db.models 모듈의 Model 클래스를 상속 받음
class Article(models.Model):
    # DB의 column을 정의
    title = models.CharField(max_length=10)
    content = models.TextField()
    # auto_now_add : 레코드의 최초 생성 일자
    created_at = models.DateTimeField(auto_now_add=True)
    # auto_now : 레코드의 최종 수정 일자
    updated_at = models.DateTimeField(auto_now=True)
```



# Migration

- Django가 model의 변화를 반영하는 방법

```bash
# model 변경사항에 대해 migration을 생성
$ python manage.py makemigrations

# migration을 DB에 반영 (동기화)
$ python manage.py migrate

# 0001이라는 migration이 SQL문으로 어떤 동작을 하는지 확인
$ python manage.py sqlmigrate app_name 0001

# migation의 적용여부를 확인
$ python manage.py showmigrations

# vscode의 SQLite 확장프로그램 이용해 DB 시각적으로 확인 가능
```



# DB API

- DB를 조작하기 위한 도구
- shell_plus를 이용해 접근
  1. 라이브러리 설치 : `pip install ipython`, `pip install django-extensions`
  2. `INSTALLED_APPS`에 `'django_extensions'` 등록
  3. `python manage.py shell_plus`

```shell
# ClassName.Manager.QuerySet_API
Article.objects.all()
```

- Manager
  - model에 query 작업이 제공되는 인터페이스
  - 기본적으로 모든 django 모델 클래스에 objects하는 manager 존재
- QuerySet
  - 데이터베이스로부터 전달받은 객체 목록
  - 조회, 필터, 정렬 등을 수행할 수 있음



# CRUD

- Create, Read, Update, Delete
