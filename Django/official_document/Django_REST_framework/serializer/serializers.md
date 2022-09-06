# Serializers

> serializer의 유용성을 확장하고자 한다. 그러나 이건 사소한 문제가 아니라, 심도있는 설계가 필요하다.
>
> *— Russell Keith-Magee,* Django users group

Serializer는 quertset이나 모델 인스턴스와 같은 complex data를 `JSON`, `XML` 같은 타입으로 쉽게 렌더링할 수 있는 기본 Python 데이터 유형으로 변환해준다. Serializer은 또한 deserialization을 제공해, 들어오는 데이터의 유효성을 검사한 뒤 파싱된 데이터를 complex type으로 변환해준다.

REST 프레임워크의 serializer는 Django의 `Form`이나 `ModelForm` 클래스와 아주 비슷하게 동작한다. 주어진 Serializer 클래스는 response의 output을 컨트롤할 강력하고도 일반적인 방법을 제공한다. 뿐만 아니라 ModelSerializer 클래스는 모델 인스턴스와 queryset을 다루는 유용한 지름길을 제공한다.

<br>

# Declaring Serializers

예시로 사용할 수 있는 간단한 객체를 만들어 시작해본다:

```python
from datetime import datetime

class Comment:
    def __init__(self, email, content, created=None):
        self.email = email
        self.content = content
        self.created = created or datetime.now()

comment = Comment(email='leila@example.com', content='foo bar')
```

Comment 객체 데이터를 serialize 혹은 deserialize 할 수 있는 serializer를 선언한다.

serializer를 선언하는 것은 form을 선언하는 것과 굉장히 유사하다:

```python
from rest_framework import serializers

class CommentSerializer(serializers.Serializer):
    email = serializers.EmailField()
    content = serializers.CharField(max_length=200)
    created = serializers.DateTimeField()
```

<br>

# Serializing objects

이제, comment나 comment list를 serialize하는 데 `CommentSerializer`를 사용할 수 있다. `Serializer` 클래스를 사용하는 것도 `Form`클래스를 사용하는 것과 비슷하다.

```python
serializer = CommentSerializer(comment)
serializer.data
# {'email': 'leila@example.com', 'content': 'foo bar', 'created': '2016-01-27T15:17:10.375877'}
```

이번엔 모델 인스턴스를 Python 기본 데이터 타입으로 바꿔본다. serialization 프로세스를 마치기 위해 데이터를 `json`으로 렌더링한다.