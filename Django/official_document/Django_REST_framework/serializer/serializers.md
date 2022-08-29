# Serializers

> serializer의 유용성을 확장하고자 한다. 그러나 이건 사소한 문제가 아니라, 심도있는 설계가 필요하다.
>
> *— Russell Keith-Magee,* Django users group

Serializer는 quertset이나 모델 인스턴스와 같은 complex data를 `JSON`, `XML` 같은 타입으로 쉽게 렌더링할 수 있는 기본 Python 데이터 유형으로 변환해준다. Serializer은 또한 deserialization을 제공해, 들어오는 데이터의 유효성을 검사한 뒤 파싱된 데이터를 complex type으로 변환해준다.

REST 프레임워크의 serializer는 Django의 `Form`이나 `ModelForm` 클래스와 아주 비슷하게 동작한다. 주어진 Serializer 클래스는 response의 output을 컨트롤할 강력하고도 일반적인 방법을 제공한다. 뿐만 아니라 ModelSerializer 클래스는 모델 인스턴스와 queryset을 다루는 유용한 지름길을 제공한다.