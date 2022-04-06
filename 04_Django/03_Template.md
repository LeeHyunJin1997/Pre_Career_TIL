# Django Template Language (DTL)

- Django template에서 사용하는 built-in template system
- 조건, 반복, 변수, 필터 등의 기능을 제공
- Python을 사용하는 로직이 아니라, 표현을 위해 일부 구조를 차용한 것 



# DTL Syntax

1. Variable

```python
# urls.py

urlpatterns = [
	path('greeting/', views.greeting)
]
```

```python
# views.py
# 변수를 정의해 template 파일로 넘김
# render()의 세번째 인자로 딕셔너리를 넘겨줌

def greeting(request):
    foods = {'apple', 'banana', 'coconut',}
    info = {
        'name': 'Alice',
    }
    context = {
        'foods': foods,
        'info': info,
    }
    return render(request, 'greeting.html', context)
```

```django
<!-- greeting.html -->
<!-- dot(.)을 사용하여 변수에 접근할 수 있음 -->

<p>안녕하세요 저는 {{ info.name }} 입니다.</p>
<p>제가 좋아하는 음식은 {{ foods }} 입니다.</p>
<p>{{ foods.0 }}을 가장 좋아합니다.</p>
```



2. Filters

```python
# urls.py

urlpatterns = [
	path('dinner/', views.dinner)
]
```

```python
# views.py

def dinner(request):
    foods = ['족발', '햄버거', '치킨', '초밥',]
    pick = random.choice(foods)
    context = {
        'pick': pick,
        'foods': foods,
    }
    return render(request, 'dinner.html', context)
```

```django
<!-- dinner.html -->
<!-- 변수를 변형, 수정 가능 -->
<!-- 60개의 built-in template filters를 제공 -->

<h1>오늘 저녁은 {{ pick }}</h1>
<p>{{ pick }}은 {{ pick|length }}글자</p>
<p>{{ foods|join:", "}}</p>
```



3. Tags

```python
# urls.py

urlpatterns = [
	path('dinner/', views.dinner)
]
```

```python
# views.py

def dinner(request):
    foods = ['족발', '햄버거', '치킨', '초밥',]
    pick = random.choice(foods)
    context = {
        'pick': pick,
        'foods': foods,
    }
    return render(request, 'dinner.html', context)
```

```django
<!-- dinner.html -->
<!-- 태그를 이용해 반복 또는 논리 수행 -->

<p>메뉴판</p>
<ul>
    {% for food in foods %}
      	<li>{{ food }}</li>
    {% endfor %}
</ul>
```



4. Comments

```django
{# 한줄 주석 #}

{% comment %}
	여러줄 주석
	여러줄 주석
{% endcomment %}
```



# Template inheritance (상속)

- 템플릿을 상속하여 재사용할 수 있음
- 하위 템플릿이 일부(블록)를 재정의(override) 할 수 있음
- 상속 방법

​		1. 상위 폴더에 `templates/` 생성

​		2. `templates/` 아래 상속할 템플릿(html) 생성

```django
<!-- base.html -->
<!-- 하위템플릿이 오버라이드 가능한 구역 지정 -->

{% block content %}
{% endblock %}
```

​		3. `settings.py`의 TEMPLATES 리스트 DIRS 속성에 템플릿 경로 추가

```python
# settings.py

TEMPLATES = [
    {
        '...': '...',
        'DIRS': [BASE_DIR / 'templates'],
        '...': ...,
    }
]
```

​		4. 하위템플릿에서 상속

```django
<!-- index.html -->
<!-- extends 태그는 반드시 최상단에 위치 -->

{% extends 'base.html' %}

{% block content %}
	<h1>만나서 반가워요!</h1>
{% endblock %}
```



- include tag

```django
<!-- templates/_nav.html -->
<!-- include되는 템플릿은 파일명 앞 _으로 구분 -->

<nav class="navbar navbar-light bg-light">
	<div class="container-fluid">
        <a class="navbar-brand" href="#">Navbar</a>
    </div>
</nav>
```

```django
<!-- templates/base.html -->
<!-- include 태그를 이용해 base.html에 _nav.html 포함시키기 -->

<body>
    {% include '_nav.html' %}
</body>
```

