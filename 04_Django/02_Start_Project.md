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



### 프로젝트 폴더 구조

```
project1/
    manage.py
    firstpjt/
        __init__.py
        settings.py
        urls.py
        asgi.py
        wsgi.py
```

- `manage.py` : 프로젝트와 같은 위치에 존재, 프로젝트와 상호작용하는 커맨드라인 유틸리티
- `firstpjt/asgi.py` : 애플리케이션과 비동기식 웹 서버의 연결 및 소통을 도움
- `firstpjt/settings.py` : 애플리케이션의 모든 설정
- `firstpjt/urls.py` : 특정 url과 views의 연결을 지정

- `firstpjt/wsgi.py` : 애플리케이션과 웹서버의 연결 및 소통을 도움



 