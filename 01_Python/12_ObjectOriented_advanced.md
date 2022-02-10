# 추상화

- 현실 세계를 프로그램 설계에 반영



# 상속

- `class NewClass(Parents):` 클래스 선언 시에 부모 클래스를 상속
- 두 클래스 사이 부모-자식 관계를 맺는 것
- 상속을 통해 메서드를 재사용하기 위함
  - 부모클래스의 모든 요소가 상속됨
  - super()를 통해 부모 클래스 요소를 호출할 수 있음

- 메서드 오버라이딩을 통해 자식 클래스에서 재정의 가능



# 상속 관련 함수와 메서드

- `issubclass(object, classinfo)` : 상속 여부를 확인 가능, classinfo의 인스턴스이거나 subclass인 경우 True 반환
  - classinfo은 튜플일 수 있고, classinfo의 모든 항목을 검사하게 됨
- `super()` : 자식 클래스에서 부모 클래스 사용
- `.mro()` : Method Resolution Order. 해당 인스턴스의 클래스가 어떤 부모 클래스를 갖는지 확인
  - 해당 클래스가 참조하는 순서대로 출력




# 다중상속

- 두 개 이상의 클래스를 상속 받는 경우
- 상속 받은 모든 클래스의 요소를 활용 가능함
- 중복된 요소들을 상속 순서에 의해 결정됨



# 다형성(Polymorphism)

- 여러 모양을 뜻하는 그리스어
- 동일한 메서드가 클래스에 따라 다르게 행동할 수 있음을 의미



# 메서드 오버라이딩

- 다형성이란 개념에 의해 메서드 오버라이딩이 가능
- 상속 받은 메서드를 재정의
  - 부모 클래스에서 정의한 메서드를 자식 클래스에서 변경
  - 특정 기능을 바꾸고 싶을 때 사용
  - 상속받은 클래스에서 같은 이름의 메서드로 덮어씀



# 캡슐화 

- 특성이나 메서드를 묶는 작업

- 은닉성 : 객체의 구형 내용에 대해 외부로부터의 직접적인 엑세스를 차단

- 응집도 : 모듈 중 자주 쓰는 것끼리 뭉쳐있음, 높을수록 좋음

- 결합도 : 모듈 간 의존성이 있음, 낮을수록 좋음

- 암묵적으로만 존재, 언어적으로 존재하지 않음

- Public Member
  - 언더바 없이 시작하는 메서드나 속성
  - 어디서나 호출 가능, 하위 클래스의 override 허용
  
- Protected Member
  - 언더바 1개로 시작하는 메서드나 속성
  - '암묵적 규칙에 의해' 부모 클래스 내부와 자식 클래스에서만 호출
    - 파이썬에서는 외부에서 접근해도 오류가 나지는 않음
  - 하위클래스 override 허용
  
- Private Member
  - 언더바 2개로 시작하는 메서드나 속성
  - 본 클래스 내부에서만 사용가능
  - 하위클래스 상속 및 호출, 외부 호출 불가능 (오류)
  - 내부적으로는  `__method()`의 이름이 name mangling
    - name mangling : `_class__method()`로 바뀜
    - 사실 `_class__method()`로는 접근가능
  
- 변수에 접근하기 위한 메서드

  ```python
  
  class classname:
      @property 
      def name(self): # getter : 변수의 값을 읽음
          return self.__name
  
  
      @name.setter
      def name(self, new_name): # setter : 변수의 값을 설정
          self.__name = new_name
      
  hyun.name = 'hyun' # 메서드를 속성처럼 사용가능
  print(hyun.name)
  ```

  