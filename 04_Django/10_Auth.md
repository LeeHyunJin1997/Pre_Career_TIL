# Django Authentication System

> Django 인증 시스템
>
> 인증(Authentication)과 권한(Authorization)을 함께 처리함
>
> - 인증 : 사용자가 누구인지 확인
> - 권한 : 인증된 사용자가 할 수 있는 작업을 결정
>
> 내부적으로 accounts라는 이름으로 관리되어 앱이름을 accounts로 지정하는 것을 권장

```python
# settings.py에 기본적으로 추가되어있음

INSTALLED_APPS = [
    ...,
    'django.contrib.auth',			# 인증 프레임워크의 핵심과 기본 모델을 포함
    'django.contrib.contenttypes',	# 사용자가 생성한 모델과 권한을 연결
    ...,
]
```

<br>

---

<br>

# 쿠키와 세션

### HTTP

> 웹에서 여러 자원, 데이터를 가져오는 일종의 규칙(프로토콜)
>
> 특징
>
> - 비연결지향 : 요청과 응답이 이루어진 후 연결은 끊김
> - 무상태 : 연결이 끊기면 통신도 끝나며 정보가 유지되지 않음



### 쿠키

> 서버가 사용자에게 전송하는 작은 기록 정보 파일
>
> 로컬에 KEY-VALUE 형식으로 저장
>
> 동일한 서버에 재요청시 저장된 쿠키를 함께 전송

#### 쿠키의 사용목적

- 세션 관리 : 로그인, 아이디 자동 완성, 장바구니 ...
- 개인화 : 사용자 테마 등의 설정
- 트래킹 : 사용자 행동 기록 및 분석

#### 수명

- Session cookies : 현재 세션이 종료되면 삭제
- Persistent cookies : 지정된 기간이 지나면 삭제



### 세션

> 사이트와 사용자 사이의 상태를 유지시키는 것
>
> 클라이언트가 서버에 접속하면 서버는 session id를 발급하고 클라이언트는 받은 session id를 쿠키에 저장

```python
# Django에서는 settings.py의 MIDDLEWARE를 통해 관리
# database-backed sessions 저장 방식이 기본값
# 모든 것을 세션으로 관리하면 사용자가 많을 때 서버에 부하가 걸릴 수 있음

# 미들웨어: 요청과 응답의 사이에서 중개해주는 시스템
MIDDLEWARE = [
    ...,
    'django.contrib.sessions.middleware.SessionMiddleware',
    ...,
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    ...,
]
```

<br>

---

<br>

# 로그인

> 인증에 관한 built-in forms 사용

```python
# accounts/urls.py

path('login/', views.login, name='login'),
```

```python
# accounts/views.py

from django.shortcuts import render, redirect
# view 함수 login와 혼동을 막기위해 이름을 붙여 사용
from django.contrib.auth import login as auth_login
from django.contrib.auth.forms import AuthenticationForm
from django.views.decorators.http import require_http_methods

# Create your views here.
@require_http_methods(['GET', 'POST'])
def login(request):
    if request.method == 'POST':
        # 요청과 요청의 정보가 순서대로 인자로 들어감
        form = AuthenticationForm(request, request.POST)
        if form.is_valid():
            # 세션의 user의 ID를 저장
            # get_user() 메서드를 이용하여 AuthenticationForm에서 user 정보를 가져올 수 있음
			# 유효성 검사를 통과했을 경우에만 user 정보 반환
            auth_login(request, form.get_user())
            return redirect('articles:index')
    else:
        form = AuthenticationForm()
    context = {'form': form,}
    return render(request, 'accounts/login.html', context)
```

```django
<!-- accounts/templates/accounts/login.html -->

{% extends 'base.html' %}

{% block content %}
  <h1>로그인</h1>
  <form action="{% url 'accounts:login' %}" method="POST">
    {% csrf_token %}
    {{ form.as_p }}
    <input type="submit">
  </form>
{% endblock content %}
```



### 로그인 정보 출력

> context processors에서 자동으로 호출가능한 데이터 목록 제공

```python
# settings.py

# 기본으로 포함되어 있는 유저 정보
TEMPLATES = [
    {
        ...,
        'OPTIONS': {
            'context_processors': [
                ...,
                'django.contrib.auth.context_processors.auth',
            ]
        }
    }
]
```

```django
<!-- base.html -->

...
<!-- user는 context_processors에서 기본 제공하는 변수, 현재 로그인된 유저 정보 출력
로그인되지 않은 상태라면, 유저 이름은 AnonymousUser -->
<h3>Hello, {{ user }}</h3>
<a href="{% url 'accounts:login' %}">Login</a>
...
```



<br>

---

<br>

# 로그아웃

```python
# accounts/urls.py

path('logout/', views.logout, name='logout'),
```

```python
# accounts/views.py

@require_POST
def logout(request):
    auth_logout(request)
    return redirect('articles:index')
```

```django
<!-- base.html -->

<form action="{% url 'accounts:logout' %}" method="POST">
    {% csrf_token %}
    <input type="submit" value="Logout">
</form>
```



사용자인증 52p부터..