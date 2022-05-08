# Foreign Key

> 외래 키
>
> 다른 테이블의 행을 식별할 수 있는 키
>
> 외래 키의 값이 부모테이블의 Primary Key일 필요는 없지만 유일한 값이어야 함 (참조 무결성)



### Foreign Key 선언

```python
# articles/modles.py

class Comment(models.Model):
    # 필드명은 참조하는 클래스 이름의 소문자(단수형), comment.article_id 로 접근 가능
    # 부모테이블과 on_delete는 필수 인자
    article = models.ForeignKey(Article, on_delete=models.CASCADE)
    content = models.CharField(max_length=200)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def __str__(self):
        return self.content
```

#### on delete

> 부모객체가 사라졌을 때 그것을 참조하던 객체를 어떻게 처리할지에 대한 정의

- `CASCADE` : 이를 참조하는 객체도 삭제

- `PROTECT` : 참조당하고 있는 부모객체가 사라지지 않도록 `ProtectedError`발생

- `RESTRICT` : 참조당하고 있는 부모객체가 사라지지 않도록 `RestrictedError` 발생

- `SET_NULL` : 해당 외래키 값을 `NULL`로 변경, `null=True` 인자를 함께 넘겨줘야만 가능

- `SET_DEFAULT` : 해당 외래키 값을 default값으로 변경, `default` 인자를 설정해줘야 가능

- `SET()` :해당 외래키 값을 SET 안에 설정된 함수에 의해 결정

- `DO_NOTHING` : 그냥 둔다. 참조 무결성을 해칠 위험이 있다

  

### 참조와 역참조

- 참조(`comment.article`) : 자식객체(N)에서 부모객체(1)를 참조
- 역참조(`article.comment_set`) : 부모객체(1)에서 자식객체(N)를 참조
  - `comment_set`은 `Article` 클래스에 실제로 존재하는 관계나 필드가 아님

```python
# articles/models.py

class Comment(models.Model):
    # related_name 옵션으로 comment_set의 호출명을 바꾸어줄 수 있음
    # 변경 후 article.comment_set은 더이상 사용 불가
    article = models.ForeignKey(Article, on_delete=models.CASCADE, related_name='comments')
```



# Comment

> 1 : N에서 N에 해당하는 Comment CRUD

- Create

```python
# articles/forms.py

class CommentForm(forms.ModelForm):

    class Meta:
        model = Comment
        # 제외해주지 않으면 ForeignKey를 Form에서 사용자가 직접 입력
       	exclude = ('article',)
```

```python
# articles/urls.py

path('<int:pk>/comments/', views.comments_create, name='comments_create'),
```

```python
# articles/views.py

# require_safe: GET 혹은 HEAD 요청만 반응하는 데코레이터, 안전한 요청
@require_safe
def detail(request, pk):
    article = get_object_or_404(Article, pk=pk)
    comment_form = CommentForm()
    context = {
        'article': article,
        'comment_form': comment_form,
    }
    return render(request, 'articles/detail.html', context)


@require_POST
def comments_create(request, pk):
    # 인증된 사용자만 생성가능
    if request.user.is_authenticated:
        article = get_object_or_404(Article, pk=pk)
        comment_form = CommentForm(request.POST)
        if comment_form.is_valid():
            # commit=False: comment_form 객체는 생성하나, 데이터베이스에 반영(저장)하지 않음
            comment = comment_form.save(commit=False)
            # 이러한 조작을 위한 객체 생성
            comment.article = article
            comment.save()
        return redirect('articles:detail', article.pk)
    # 인증된 사용자가 아니라면 로그인부터
    return redirect('accounts:login')
```

```django
<!-- articles/detail.html -->

{% extends 'base.html' %}

{% block content %}
    <hr>
    <form action="{% url 'articles:comments_create' article_pk %}" method=POST>
        {% csrf_token %}
        {{comment_form}}
        <input type="submit">
    </form>
{% endblock content %}
```



- Read

```python
# articles/views.py

@require_safe
def detail(request, pk):
    article = get_object_or_404(Article, pk=pk)
    comment_form = CommentForm()
    comments = article.comment_set.all()
    context = {
        'article': article,
        'comment_form': comment_form,
        'comments': comments,
    }
    return render(request, 'articles/detail.html', context)
```

```html
<!-- articles/detail.html --> 

<hr>
<h4>댓글 목록</h4>
<ul>
    {% for comment in comments %}
    	<li>{{ comment.content }}</li>
    {% endfor %}
</ul>
```



- Delete

```python
# articles/urls.py

path('<int:article_pk>/comments/<int:comment_pk>/delete/', views.comments_delete,
     name='comments_delete'),
```

```python
# articles/views.py

@require_POST
def comments_delete(request, article_pk, comment_pk):
    # 인증된 사용자만 삭제 가능
    if request.user.is_autheticated:
        comment = get_object_or_404(Comment, pk=comment_pk)
        comment.delete()
    return redirect('articles:detail', article_pk)
```

```html
<!-- articles/detail.html -->

<h4>댓글 목록</h4>
{% if comments %}
  <p><b>{{ comments|length }}개의 댓글이 있습니다.</b></p>
{% endif %}
<ul>
  {% for comment in comments %}
    <li>
      {{comment.content}}
      <form action="{% url 'articles:comments_delete' article.pk comment.pk %}" method="POST" class="d-inline">
        {% csrf_token %}
        <input type="submit" value="DELETE">
      </form>
    </li>
  {% empty %}
    <p>댓글이 없어요..</p>
  {% endfor %}
</ul>
```



# 1:N 모델

```python
# articles/models.py

class Article(models.Model):
    # 기존 모델에 user 필드 추가
    user = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
    title = models.CharField(max_length=10)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def __str__(self):
        return self.title
```

```python
# articles/forms.py

class ArticleForm(forms.ModelForm):

    class Meta:
        model = Article
        # '__all__'이던 필드를 변경하여
        # 추가된 user 필드가 article을 생성할 form에 드러나는 것을 방지
        fields = ('title', 'content',)
```

```python
# articles/views.py

@login_required
@require_http_methods(['GET', 'POST'])
def create(request):
    if request.method == 'POST':
        form = ArticleForm(request.POST)
        if form.is_valid():
            # 단, user 필드를 입력받지 않으면
            # NOT NULL consrtaint failed 에러 발생
            # 따라서 save 전에 article의 user를 자동으로 지정해주는 작업 추가
            article = form.save(commit=False)
            article.user = request.user
            article.save()
            return redirect('articles:detail', article.pk)
    else:
        form = ArticleForm()
    context = {
        'form': form,
    }
    return render(request, 'articles/create.html', context)
```



p. 81
