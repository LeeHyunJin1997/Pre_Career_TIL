# Django 시작하기

### 가상환경 활성화

- `python -m venv venv` : 해당 폴더에 venv라는 이름의 가상환경 생성
- `source venv/Script/activate` : 가상환경 활성화



### 프로젝트 시작하기

- `pip install django==3.2.12` : Django 설치 (버전 설정)
- `django-admin startproject firstpjt .` : firstpjt 라는 프로젝트 폴더 생성 
  - 끝에 `.` 을 붙이지 않으면 폴더 안에 폴더 생성
- `python manage.py runserver` : 서버 활성화
- 여기까지 마친 후 서버 주고를 열어보면, Django 페이지와 로켓 이미지가 보인다

```python
# 프로젝트 구조
project1/
    manage.py	# 프로젝트와 같은 위치에 존재, 프로젝트와 상호작용하는 커맨드라인 유틸리티
    firstpjt/
        __init__.py
        settings.py	# 애플리케이션의 모든 설정
        urls.py		# 특정 url과 views의 연결을 지정
        asgi.py		# 애플리케이션과 비동기식 웹 서버의 연결 및 소통을 도움
        wsgi.py		# 애플리케이션과 웹서버의 연결 및 소통을 도움
```

- 자주 사용하는 `settings.py` 의 설정
  - `INSTALLED_APPS`
  - `LANGUAGE_CODE = 'ko-kr'` : 사용자에게 제공되는 번역을 결정
  - `TIME_ZONE = Asia/Seoul`  : 데이터베이스의 기준 시간을 서울로 설정



### 애플리케이션 생성

- `python manage.py startapp articles` : articles라는 애플리케이션 생성
- 실제 요청을 처리하고 페이지를 보여주는 역할
- 일반적으로 앱은 하나의 기능 단위로 작성
- 하나의 프로젝트는 여러 앱을 가짐

```python
# 애플리케이션 구조
project1/
    articles/
        migrations/
        (+templates/)		# templates를 추가해 서식(html)을 지정, html을 탐색하는 기본경로
        	(+articles/)	# 애플리케이션의 폴더를 이중구조로 만들어 다른 애플리케이션 서식과 구분
        __init__.py
        admin.py
        apps.py				# 앱의 정보 작성
        models.py			# 앱에서 사용하는 Model을 정의
        tests.py			# 프로젝트의 테스트 코드를 작성
        views.py			# view 함수들을 정의
        (+urls.py)			# include 함수를 써서 애플리케이션의 urls를 사용 가능
```



### 애플리케이션 사용

1. 앱을 생성한 후에는 반드시 settings.py의 INSTALLED_APPS 리스트에 등록해야함

   - 생성 후 등록의 순서 지킬 것

   - INSTALLED_APPS 리스트의 항목은 Local apps - Third party apps - Django apps 의 순서로 작성

2. 프로젝트 혹은 애플리케이션의 urls.py에 특정 url과 view를 연결 (HTTP 요청을 알맞은 view로 전달)

   ```python
   from django.contrib import admin
   from django.urls import path
   from articles import views
   
   urlpatterns = [
       path('admin/', admin.site.urls),
       path('index/', views.index),	# Django는 리스트 마지막 항목에 ,를 붙이는 것을 권장
   ]
   ```

3. 애플리케이션의 views.py 에 HTTP 요청을 수신하고 응답을 반환하는 함수 작성

   ```python
   from django.shortcuts import render
   
   def index(request):							# index 요청이 발생하면,
       return render(request, 'index.html')	# index.html로 이동
   ```

