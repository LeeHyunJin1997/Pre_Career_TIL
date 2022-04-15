# Form

> 기존의 HTML form은 사용자가 입력한 정보가 옳은지 확인하는 '유효성 검사' 과정이 복잡함
>
> Django는 유효성 검사를 단순화하고 자동화한 Form 기능을 제공





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

<br>

---

<br>

# ModelForm

> Model에서 정의한 필드를 Form에서 재정의하는 행위를 막기 위한 도구
>
> 이미 생성된 Model을 이용해 Form을 만듦

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

```python
# articles/views.py

def create(request):
    form = ArticleForm(request.POST)
    # is_valid(): 데이터가 유효한지 여부를 boolean으로 반환
    if form.is_valid():
        article = form.save()
        return redirect('articles:detail', article.pk)
    return redirect('articles:new')
```



FORM 24p부터























































