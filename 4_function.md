# 함수

- 특정한 기능을 하는 코드의 묶음
- 특정 명령을 수행하는 코드를 다시 작성하지 않고, 필요 시 호출



### 추상화(Abstraction)

복잡한 내용을 모르더라고 사용할 수 있도록(블랙박스)

재사용성과 가독성, 생산성



### 함수 기본 구조

- 선언과 호출
  - 함수명() 으로 호출
  - parameter가 있는 경우, 인자값을 넣어 호출
- 입력
  - Parameter : 함수를 실행할 때, 함수 내부에서 사용되는 식별자
  - Argument : 함수 호출 시 전달되는 값
    - 필수 Argument
    - 선택 Argument
      - 선택 Argument가 앞에 나오면 위치가 깨져버리기 때문에, 반드시 뒤쪽에 선언
    - Positional Arguments : 위치에 따라 Arguments를 전달하는 방법.  Default한 형식
    - Keyword Arguments : 변수명으로 Arguments를 지정하는 방법
      - Keyword로 지정한 이후의 Arguments는 마찬가지로 지정해야함
  - Argument 수를 지정하지 않고 전달받고 싶을 때는 패킹/언패킹 연산자 활용

```python
def add(x) #필수 Argument

def add(x=1) #선택 Argument

def function(ham): # patameter : ham
    return ham

function('spam') # argument : 'spam'

def add(x,y):
    return x+y

add(2,5) #Positionnal Arguments

add(x=2,y=5) #Keyword Arguments

def add(*args): #패킹 연산자

def family(**kwagrs): #dictionary로 패킹
```



- 문서화
- 범위(Scope)
  - Built-in scope : 실행된 이후 영원히 존재
  - Global scope : 코드 어디에서든 참조 가능, 한 파일(.py) 내에서 변수 유지
  - Enclosed scope
  - Local scope : 함수 내의 공간, 함수를 동작하고 변수는 사라짐
  - 더 작은 범위에서부터 변수를 찾게됨
  - 더 작은 범위에서 큰 범위 변수에 접근할 수는 있지만, 수정할 수는 없음
    - global을 수정하고 싶을 때는 `global` 사용
    - 가장 가까운 범위의 변수를 수정할 때는 `nonlocal` 사용
    - 단, 변경사항의 추적과 유지보수가 어렵기 때문에 사용을 권장하지 않음
- 결과값
  - Void function : return 값이 없음. None을 반환하고 종료
  - Value returning function : 실행 후, 특정 값을 반환하는 함수 
  - 함수는 단일 값만을 반환하므로, 두 개이상의 값이 필요하다면 튜플을 이용