# Static File

- 응답할 때 별도의 처리 없이 내용을 그대로 보여주는 파일
- 파일이 고정되어 있고, 서비스 중에도 추가, 변경되지 않음
- 이미지, CSS ...
- `STATIC_ROOT` : Django에서 사용하는 모든 Static file을 모아놓는 절대경로
  - 배포 단계에서 사용됨 (`DEBUG = Flase`)

```python
# settings.py
# Django는 기본적으로 static file을 별도 관리하고 있음

INSTALLED_APPS = [
    '...',
    'django.conteib.staticfiles',
]

# 탐색할 기본경로(app/static), 경로 추가 
STATICFILES_DIRS = [
    BASE_DIR / 'static',
]

# STATIC_ROOT의 정적 파일을 참조할 URL
# 실제 파일이나 디렉토리가 아님
STATIC_URL = '/static/'

# STATIC_ROOT 경로 지정
# 경로를 지정한 후 python manage.py collectstatic으로 사용된 정적 파일들을 수집할 수 있음
STATIC_ROOT = BASE_DIR / 'staticfiles'
```

```django
<!-- static file 불러오기 -->

<!-- built-in tag가 아니기 때문에 load 필요>
{% load static %}
<!-- static file도 template처럼 app/static/app 구조에 위치 -->
<img src="{% static 'my_app/example.jpg' %}" alt="My Image">
```

