```python
# urls.py

urlpatterns = [
    ...,
    path('throw/', views.throw),
]
```

```python
# view.py

def throw(request):
    return render(request, 'throw.html')
```

```django
<!-- throw.html -->

{% extends 'base.html' %}

{% block content %}
	<h1>Throw</h1>
	<form action="#" method="#">
        <label for="message">Throw</label>
        <input type="text" id="message" name="message">
        <input type="submit">
	</form>
{% endblock %}
```

- form : 사용자로부터 받은 데이터를 서버로 전송
  - `action` : 입력 데이터가 전송될 url 지정
  - `method` : 입력데이터의 전달 방식
    - GET (default)
    - POST



- label
  - 사용자 인터페이스 항목에 대한 설명
  - `for` : 일치하는 `id`를 가진 첫번째 요소를 제어



- input

  - 사용자로부터 데이터를 입력 받음
  - `type` : input의 유형 지정
    - text
    - submit
    - ...
  - `name` : 서버에 전달되는 URL 형태를 결정
    - name은 key, 입력받은 값은 value로 매핑
    - ?key=value&key=value
  - `id` : label의 `for`와 일치시켜 연결

  