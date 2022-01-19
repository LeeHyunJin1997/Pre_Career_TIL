# 내장함수



## map(함수, iterable)

- 순회가능(iterable)한 데이터의 모든 요소에 함수를 적용



## filter(함수, iterable)

- 순회가능(iterable)한 모든 요소에 함수를 적용해, True인 것만 반환



## zip(*iterables)

- 복수의 iterable을 모아 튜플을 원소로 하는 zip object를 반환



## lambda 함수

- 익명함수
- 간단한 함수만 표현 가능
  - return문을 가질 수 없음
  - 간편 조건문 외의 조건문이나 반복문을 가질 수 없음
- def를 사용할 수 없는 곳에서도 사용 가능
- `lambda 매개변수 : 리턴값` 의 문법



## 재귀함수(recursive function)

- 자기 자신을 호출하는 함수
- 1개 이상의 base case(종료 상황)가 존재하고, 수렴하도록 작성
  - 예) 3! = 3 * 2!
- 메모리 스택이 넘치면(stack overflow) 프로그램이 동작하지 않는다
- 파이썬은 최대 재귀 깊이를 1000번으로 제한
- 반복문에 비해 변수 사용을 줄일 수 있음
- 단, 입력값이 커지면 느려짐