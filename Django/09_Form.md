# Form

> 기존의 HTML form은 사용자가 입력한 정보가 옳은지 확인하는 '유효성 검사' 과정이 복잡함
>
> Django는 유효성 검사를 단순화하고 자동화한 Form 기능을 제공
>
> 어떤 Model에 저장해야 하는지 알 수 없으므로 유효성 검사 후 cleaned_data 딕셔너리를 생성



### Form 사용하기

```python
# articles/forms.py

from django import forms

# Form 선언 (Model 선언과 유사)
# forms 라이브러리에서 파생된 Form 클래스를 상속
class ArticleForm(forms.Form):
    title = forms.CharField(max_length=10)
    content = forms.CharField()
```

```python
# articles/views.py

from .forms import ArticleForm

# form 객체를 생성해 context로 넘김
def new(request):
    form = ArticleForm()
    context = {'form': form}
    return render(request, 'articles/new.html', context)
```

```django
<!-- new.html -->

{% extends 'base.html' %}

{% block content %}
  <h1>NEW</h1>
  <hr>
  <form action="{% url 'articles:create' %}" method="POST">
    {% csrf_token %}
  	<!-- HTML form으로 표현하던 양식을 form.as_p로 대체 -->
    {{ form.as_p }}
    <input type="submit">
  </form>
{% endblock content %}
```



### Form rendering options

- as_p : 각 필드가 `<p>` 태그로 감싸져서 렌더링
- as_ul : 각 필드가 `<li>` 태그로 감싸져서 렌더링
  - `<ul>` 태그는 따로 작성 
- as_table : 각 필드가 `<tr>` 태그로 감싸져서 렌더링
  - `<table>` 태그는 따로 작성 



### Widgets

> HTML의 input 요소를 렌더링
>
> 반드시 From Fields 내에 할당
>
> Form Fields는 input의 유효성 검사를 처리하는 반면, Widgets은 단순히 형태만 지정

```python
# articles/forms.py

class ArticleForm(forms.Form):
    REGION_A = "sl"
    REGION_B = "dj"
    REGION_C = "gj"
    REGION_D = "gm"
    REGION_E = "bu"
    REGIONS_CHOICES = [
        (REGION_A, '서울'),
        (REGION_B, '대전'),
        (REGION_C, '광주'),
        (REGION_D, '구미'),
        (REGION_E, '부산'),
    ]
    ...
    # 한 줄 텍스트 input을 블록형으로 변경
    content = forms.CharField(widget=forms.Textarea)
   	# 지역을 선택하는 선택형 input 설정, 선택 항목은 choices 인자로 받음
    region = forms.ChoiceField(choices=REGIONS_CHOICES, widget=forms.Select())
```



### cleaned_data

```python
# Form은 Model이 지정되지 않아 cleaned_data를 이용해 전송된 form으로부터 데이터를 받아야함

def create(request):
    form = ArticleForm(request.POST)
    # 유효성 검사 후
    if form.is_valid():
        # cleaned_data를 이용해 데이터 받기
        title = form.cleaned_data.get('title')
        content = form.cleaned_data.get('content')
        # 모델 지정 후 데이터 생성
        article = Article.objects.create(title=title, content=content)
        return redirect('articles:detail', article.pk)
```

<br>

---

<br>

# ModelForm

> Model에서 정의한 필드를 Form에서 재정의하는 행위를 막기 위한 도구
>
> 이미 생성된 Model을 이용해 Form을 만듦
>
> model이 정의되어 있기 때문에 유효성검사 후 바로 .save() 가능

- Forms

```python
# articles/forms.py

from django import forms
from .models import Article

# forms 라이브러리에서 파생된 Model
class ArticleForm(forms.ModelForm):
    
    # Meta Class: 사용할 Model을 구성
    class Meta:
        model = Article
        # fields 혹은 exclude를 사용하여 필드 지정
        fields = '__all__'
        # exclude = ('title', )
```



- Create

```python
# articles/views.py
# new 삭제

def create(request):
    # POST 방식, create할 정보가 적혀서 전달되었을 때
    if request.method == 'POST':
    	form = ArticleForm(request.POST)
        # is_valid(): 데이터가 유효한지 여부를 boolean으로 반환
        if form.is_valid():
            # 데이터베이스 객체를 만들고 저장
            # instatnce 인자로 기존 모델 정보를 받아올 수 있음
            # 유효하지 않은 경우, save()를 호출하면 form.errors를 확인 가능
            article = form.save()
            return redirect('articles:detail', article.pk)
    # GET 방식, 단순히 페이지로 이동하려 할 때
    else:
        form = ArticleForm()
    context = {'form': form,}
    return render(request, 'articles/create.html', context)
```

```django
<!-- create.html -->

{% extends 'base.html' %}

{% block content %}
  <h1>CREATE</h1>
  <hr>
  <form action="{% url 'articles:create' %}" method="POST">
    {% csrf_token %}
    {{ form.as_p }}
    <input type="submit">
  </form>
  <hr>
  <a href="{% url 'articles:index' %}">BACK</a>
{% endblock content %}
```



- Delete

```python
# views.py

def delete(request, pk):
    article = Article.objects.get(pk=pk)
    if request.method == 'POST':
        article.delete()
        return redirect('articles:index')
    return redirect('articles:detail', article.pk)
```

```django
<!-- detail.html -->

...
<form action="{% url 'articles:delete' article.pk %}" method="POST">
 {% csrf_token %}
 <input type="submit" value="삭제">
</form>
...
```



- Update

```python
# view.py

def update(request, pk):
    article = Article.objects.get(pk=pk)
    if request.method == 'POST':
        # instance로 기존 정보 표출
        form = ArticleForm(request.POST, instance=article)
        if form.is_valid():
            form.save()
            return redirect('aritlces:detail', article.pk)
    else:
        form = ArticleForm(instance=article)
    context = {
        'form': form,
        'article': article,
    }
    return render(request, 'atricles/update.html', context)
```

```django
<!-- update.html -->

{% extends 'base.html' %}

{% block content %}
  <h1>UPDATE</h1>
  <hr>
  <form action="{% url 'articles:update' article.pk %}" method="POST">
    {% csrf_token %}
    {{ form.as_p }}
    <input type="submit">
  </form>
  <a href="{% url 'articles:detail' article.pk %}"></a>
{% endblock content %}
```

```django
<!-- detail.html -->

...
<a href="{% url 'articles:update' article.pk %}">UPDATE</a><br>
...
```



### Widgets

```python
class ArticleForm(forms.ModelForm):
    # 각 필드를 어떻게 보여줄지를 지정
    title = forms.CharField(
    	label='제목',
    	widget=forms.TextInput(
        	attrs={
                'class': 'my-title',
                # 클래스에 부트스트랩 form-control을 사용해 꾸며줄 수 있음
                # 'class': 'my-title form-control'
                'placeholder': 'Enter the title',
                'maxlength': 10,
            }
        ),
    )
    
    content = forms.CharField(
    	label='내용',
    	widget=forms.Textarea(
        	attrs={
                'class': 'my-content',
                'placeholder': 'Enter the content',
                'rows': 5,
                'cols': 50,
            }
        ),
    )
    
    class Meta:
        model = Article,
        fields = '__all__'
```













































