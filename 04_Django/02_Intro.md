# Django 시작하기

1. 가상환경 활성화

- `python -m venv venv` : 해당 폴더에 venv라는 이름의 가상환경 생성

- `source venv/Script/activate` : 가상환경 활성화

2. 시작하기

- `pip install django==3.2.12` : Django 설치 (버전 설정)

- `django-admin startproject firstpjt .` : firstpjt 라는 프로젝트 폴더 생성 
  - 끝에 `.` 을 붙이지 않으면 폴더 안에 폴더 생성
- `python manage.py runserver` : 서버 활성화