# Field types

### TextField

##### class TextField(**options)

긴 텍스트를 위한 필드. 이 필드를 위한 default form widget은 **Textarea**.

**max_length** 속성을 지정하면, 자동 생성된 form field의 **Textarea** widget에 반영된다. 그러나 모델이나 데이터베이스에서 시행되는 것은 아니니, 데이터베이스에서도 글자수를 제한하고 싶다면 **CharField**를 사용하라. 

<br>

##### TextField.db_collation

선택사항. 정렬 시에 사용할 방식(database collation name)을 지정한다.

> ##### Note
>
> Collation name은 표준화되지 않았다. 따라서 여러 데이터베이스 백엔드로 옮길 수는 없다.

> ##### Oracle
>
> 오라클은 **TextField**에 대해 collation을 제공하지 않는다.

<br>

---

### URLField

##### class URLField(max_length=200, **options)

URL을 위한 **CharField**, **URLValidator**로 유효성 검사된다.

이 필드를 위한 default form widget은 **URLInput**.

모든 **CharField**의 하위 클래스와 마찬가지로 **URLField**는 **max_length** 인자를 사용한다. **max_length**를 특정하지 않는다면, default로 200이 들어간다.

<br>

---