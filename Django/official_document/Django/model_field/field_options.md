# Field options

### null

##### Field.null

**True**라면, Django는 데이터베이스에 **NULL**같은 빈 값을 저장한다. Default는 **False**이다.

단, **CharField**나 **TextField** 같은 string-based field에 null을 사용하는 것은 피해야한다. string-based field가 **null=True** 옵션을 갖게되면 '데이터가 없음'을 나타내는 **NULL**과 '빈 string'이라는 2가지 값을 뜻할 수 있다. Django 컨벤션은 **NULL**이 아닌, 빈 string을 사용하도록 하고 있다. 한 가지 예외는 **CharField**가 **unique=True**와 **blank=True**의 옵션을 동시에 가지고 있을 때이다. 이 상황에서는 고유값 제약 조건을 위반하지 않고 공백으로 여러 개체를 저장하려면 **null=True** 옵션이 필요하다.

string-based이거나 non-string-based이거나, **null** 매개변수는 데이터베이스 저장소에만 영향을 끼치는 것이기 때문에, form에서 빈값을 받으려면 **blank=True**를 설정해주어야 한다.  

> 오라클 데이터베이스 백엔드를 사용한다면, 이 속성과 관계없이 빈 string을 나타내기 위해 **NULL** 값이 저장된다.

<br>

---

### blank

##### Field.blank

**True**라면, 빈칸을 허용한다. Default는 **False**이다.

**null**과는 다르다. **null**은 순전히 데이터베이스와만 연관되어 있는 반면, **blank**는 유효성 검사에 관한 것이다. **blank=True** 옵션이 있다면, form의 유효성 검사는 빈 값의 입력을 허용한다. **blank=False**일 때는 반드시 값을 입력해야 한다.

> **blank=True**는 **null=False**와 함께 사용될 수 있으나, 입력받지 않은 값을 프로그래밍적으로 넣으려면 모델에 **clean()**을 구현해야 한다.