# Variable Routing

- URL의 일부를 변수로 지정하여 view 함수의 인자로 넘김
- 하나의 `path()`에 여러 페이지를 연결시킬 수 있음
- `str` : `/`를 제외하고 비어있지 않은 모든 문자열
  - 작성하지 않을 경우 기본값
- `int` : 0 또는 양의 정수
- `slug` : ASCII 문자 또는 숫자, 하이픈 및 밑줄 문자로 구성된 모든 슬러그 문자열

```python
# urls.py

urlpatterns = [
    ...,
    path('hello/<str:name>/', views.hello),
]
```

```python
# views.py

def hello(request, name):
    context = {
        'name': name,
    }
    return render(request, 'hello.html', context)
```

```django
<!-- hello.html -->

{% extends 'base.html' %}

{% block content %}
	<h1>만나서 반가워요 {{ name }}님</h1>
{% endblock %}
```



# App URL Mapping

- 각 app마다  `urls.py`를 지정

```python
# firstpjt/urls.py
# 프로젝트의 url

from django.contrib import admin
from django.urls import path, include

# include를 이용해 다른 URLconf 모듈을 가져옴
urlpatterns = [
    path('admin/', admin.site.urls),
    path('articles/', include('articles.urls')),
]
```

```python
# articles/urls.py

from django.urls import path
from . import views

# 여러 app이 존재할 때, app_name을 이용해 각 URL을 구분할 수 있음
app_name = 'articles'
urlpatterns = [
    path('index/', views.index),
    path('greeting/', views.greeting),
    ...,
]
```



# Naming URL patterns

- 각 URL에 이름을 붙여 간편하게 URL를 재사용

```python
# articles/urls.py

urlpatterns = [
    path('index/', views.index, name='index'),
    path('greeting/', views.greeting, name='greeting'),
    ...,
]
```

```django
<!-- index.html -->

{% extends %}

{% block content %}
	<h1>만나서 반가워요</h1>
	<a href="{% url 'greeting' %}">greeting</a>
{% endblock %}
```

- Namespace를 구분하기 위해 app_name을 사용한 경우

```python
# articles/urls.py

app_name = 'articles'
urlpatterns = [
    path('index/', views.index, name='index'),
    path('greeting/', views.greeting, name='greeting'),
    ...,
]
```

```python
# articles/views.py
# 이름 공간 뿐만 아니라, 실제 폴더 공간도 구분하기 위해
# 템플릿의 위치를 articles/templates/articles/로 이동

def index(request):
    return render(request, 'articles/index.html')

def greeting(request):
    return render(request, 'articles/greeting.html')
```

```python
<!-- index.html -->

{% extends %}

{% block content %}
	<h1>만나서 반가워요</h1>
	<a href="{% url 'articles:greeting' %}">greeting</a>
{% endblock %}
```

