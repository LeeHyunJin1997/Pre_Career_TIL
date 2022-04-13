# Model

- Django는 model을 통해 데이터에 접속하고 관리
- 각각의 model은 하나의 데이터베이스 테이블에 매핑



---



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
    
    # 각 레코드를 print하면 title 속성을 반환
    def __str__(self):
        return self.title
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

- Create

```shell
# 방법 1
article = Article()
article.title = 'first'
article.content = 'django!'
article.save()

# 방법 2
article = Article(title='second', content='django!!')
article.save()

# 방법 3
Article.objects.create(title='third', content='django!')
```

- Read

```shell
# QuerySet에 포함된 전체 레코드 확인
Article.objects.all()

# 특정 속성값을 갖는 객체를 반환
Article.objects.get(pk=100)
Article.objects.get(content='django!')

# 특정 조건을 만족하는 객체의 새 QuerySet을 반환
Article.objects.filter(content='django!')
Article.objects.filter(title='first!')
```

- Update

```shell
article = Article.objects.get(pk=1)
# 현재 article.title은 'first'
article.title = 'byebye'
article.save()
```

- Delete

```shell
article = Article.objects.get(pk=1)
article.delete()
```



# Admin Site

- 서버의 관리자 페이지
- 모델을 admin.py에 등록하고 관리
- django.contrib.auth 모듈에서 제공

```bash
# 관리자 계정 생성
$ python manage.py createsuperuser
# 뒤이어 생성할 관리자 아이디, 비밀번호(보이지 않음) 입력
```

```python
# articles/admin.py

from django.contrib import admin
from .models import Article

# 등록할 모델 속성 지정
class ArticleAdmin(admin.ModelAdmin):
    # 모델이 보여줄 속성 지정
    list_display = ('pk', 'title', 'content', 'create_at', 'update_at',)
    
# 모델 등록
admin.site.register(Article, ArticleAdmin)
```



# Form 전송방식

- GET
  - URL에 Form의 내용이 그대로 노출
  - 보안에 취약하여 데이터를 가져올 때만 사용
  - CRUD 중 R에만 사용
- POST
  - 데이터를 변경할 때 사용
  - csrf token을 사용, 사용자 데이터에 난수를 부여하는 방식으로 보안 강화
    - Cross-Site Request Forgery : URL을 조작해 웹페이지의 수정, 삭제에 접근하는 공격
    - `setting.py` 의 `MIDDLEWARE`에서 csrf 관련 보안 설정



# 웹 상에서 CRUD

-  Read (index)

```python
# articles/views.py

from .models import Article

def index(request):
    articles = Article.objects.all()
    # 순서가 반대인 목록 가져오기
    # articles = Article.objects.order_by('-pk')
    # 가져와서 순서 바꾸기
    # articles = Article.objects.all()[::-1]
    
    context = {
        'articles': articles,
    }
    return render(request, 'articles/index.html', context)
```

```django
{% extends 'base.html' %}

{% block content %}
  <h1>Articles</h1>
  <a href="{% url 'articles:new' %}">NEW</a>
  <hr>
  {% for article in articles %}
    <p>글 번호: {{ article.pk }}</p>
    <p>글 제목: {{ article.title }}</p>
    <p>글 내용: {{ article.content }}</p>
    <a href="{% url 'articles:detail' article.pk %}">DETAIL</a>
    <hr>
  {% endfor %}
{% endblock content %}
```

- Create (new & create)

  - New - 새로운 article의 내용을 작성할 페이지

  ```python
  # articles/views.py
  
  def new(request):
      return render(request, 'articles/new.html')
  ```

  ``` django
  <!-- articles/templates/articles/new.html -->
  
  {% extends 'base.html' %}
  
  {% block content %}
  	<h1>NEW</h1>
  	<!-- form을 작성해 create으로 전송 -->
  	<form action="{% url 'articles:create'%}" method="POST">
          <!-- POST방식은 반드시 csrf 토큰을 포함 -->
          {% csrf_token %}
      	<label for="title">Title: </label>
          <input type="text" name="title"><br>
          <label for="content">Content: </label>
          <textarea name="content" cols="30" rows="5"></textarea><br>
          <input type="submit">
  	</form>
  	<hr>
  	<a href="{% url 'articles:index' %}"[back]</a>
  {% endblock %}
  ```

  - Create - 작성된 내용을 전달받아 모델에 입력
    - 페이지로 이동하는 것이 아니라, 입력만 하고 redirect

  ```python
  # articles/views.py
  
  from django.shortcuts import render, redirect
  
  def create(request):
      # 전송된 form에서 속성을 골라냄
      title = request.POST.get('title')
      content = request.POST.get('content')
      
      article = Article(title=title, content=content)
      article.save()
      # 저장 후에는 index 페이지로 이동
      return redirect('articles:index')
  ```

- Detail (개별 글을 선택, 이동하기 위한 페이지)

```python
# articles/urls.py

path('<int:pk>/', views.detail, name='detail'),
```

```python
# articles/views.py

def detail(request, pk):
    article = Article.objects.get(pk=pk)
    context = {
        'article': article
    }
    return render(request, 'articles/detail.html', context)
```

```django
<!-- articles/templates/articles/detail.html -->

{% extends 'base.html' %}

{% block content %}
    <h1>DETAIL</h1><hr>
    <p>제목: {{ article.title }}</p>
    <p>내용: {{ article.content }}</p>
    <p>작성시각: {{ article.created_at }}</p>
    <p>수정시각: {{ article.updated_at }}</p>
    <hr>
    <a href="{% url 'articles:index' %}">BACK</a>
{% endblock content %}
```

- Delete

```python
# articles/urls.py

path('<int:pk>/delete', views.delete, name='delete'),
```

```python
# articles/views.py

def delete(request, pk):
    article = Article.objects.get(pk=pk)
    # POST방식일 경우에만 삭제하도록 지정해 URL로 직접 삭제에 접근하려는 것을 막음
    if request.method == 'POST':
    	article.delete()
        return redirect('articles:index')
    # GET방식일 때는 detail로 돌아가기
    else:
    	return redirect('articles:detail', article.pk)
```

```django
<!-- articles/templates/articles/detail.html -->

{% extends 'base.html' %}

{% block content %}
	<!-- delete로 이동함과 동시에 article.pk 전달 -->
	<form action="{% url 'articles:delete' article.pk %}" method="POST">
        {% csrf_token %}
        <button>DELETE</button>
	</form>
	<a href="{% url 'articles:index' %}">BACK</a>
{% endblock %}
```

- Update (edit & update)

  - Edit - 수정사항을 입력받을 페이지

  ```python
  # articles/urls.py
  
  path('<int:pk>/edit/', views.edit, name='edit')
  ```

  ```python
  # articles/views.py
  
  def edit(request, pk):
      article = Article.objects.get(pk=pk)
      context = {
          'article': article,
      }
      return render(request, 'articles/edit.html', context)
  ```

  ```django
  <!-- articles/templates/articles/edit.html -->
  
  {% extends 'base.html' %}
  
  {% block content %}
  	<h1>EDIT</h1>
  	<form action="{% url 'articles:update'%}" method="POST">
          {% csrf_token %}
      	<label for="title">Title: </label>
          <!-- value값을 지정해주어 변경 전 상태를 표시 -->
          <input type="text" name="title" value="{{ article.title }}"><br>
          <label for="content">Content: </label>
          <textarea name="content" cols="30" rows="5">{{ article.content}}</textarea>
          <br>
          <input type="submit">
  	</form>
  	<hr>
  	<a href="{% url 'articles:index' %}"[back]</a>
  {% endblock %}
  ```

  - Update - 수정사항을 저장하고 detail로 이동

  ```python
  # articles/urls.py
  
  path('<int:pk>/update', views.update, name='update'),
  ```

  ```python
  # articles/views.py
  
  def update(request, pk):
      article = Article.objects.get(pk=pk)
      article.title = request.POST.get('title')
      article.content = request.POST.get('content')
      article.save()
      return redirect('articles:detail', article.pk)
  ```

  ```django
  <!-- articles/templates/articles/edit.html -->
  
  {% extends 'base.html' %}
  
  {% block content %}
  	<h1>EDIT</h1>
  	<form action="{% url 'articles:update' article.pk %}" method="POST">
          {% csrf_token %}
          ...
  	</form>
  	<a href="{% url 'articles:index' %}">BACK</a>
  {% endblock %}
  ```

  



