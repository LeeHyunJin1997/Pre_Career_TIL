# Serializing Django objects

Django의 serialization(직렬화) 프레임워크는 Django모델을 <u>다른 형식</u>로 변환하는 메커니즘을 제공한다. 일반적으로 <u>다른 형식</u>는 텍스트 기반이며, 유선으로 Django의 데이터를 보내는 데 사용한다. 하지만 serializer는 텍스트 기반이 아닌 어떤 형식이든 다룰 수 있게 해준다.

> ##### See also
>
> 테이블의 데이터를 serialize된 형식으로 가져오길 원한다면, **dumpdata** management command를 사용할 수 있다.

<br>

### Serializing data

최상위에선 다음처럼 serialize 할 수 있다:

```python
from django.core import serializers
data = serializers.serialize("xml", SomeModel.objects.all())
```

**serialize** 함수의 인자는 데이터를 serialize 할 형식과 serialize 할 **QuerySet**이다. (사실, 두 번째 인자는 Django 모델 인스턴스를 생성하는 모든 iterator가 될 수 있지만, 거의 항상 QuerySet이다.)

`django.core.serializers.get_serializer(format)`

또한 serializer object를 직접 사용할 수 있다:

```python
XMLSerializer = serializers.get_serializer("xml")
xml_serializer = XMLSerializer()
xml_serializer.serialize(queryset)
data = xml_serializer.getvalue()
```

이건 데이터를 **HttpResponse** 같은 file-like object로 직접 serialize하려는 경우, 유용하다:

```python
with open("file.xml", "w") as out:
    xml_serializer.serialize(SomeModel.objects.all(), stream=out)
```

> Note
>
> 지정되지 않은 형식으로 `get_serializer()`를 호출하는 것은 `django.core.serializers.SerializerDoesNotExist` exception을 발생시킨다.

<br>

#### Subset of fields