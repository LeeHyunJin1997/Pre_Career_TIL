# 디버깅

### 주된 오류

- Syntax error : 문법 오류

- branches : 모든 조건이 원하는대로 동작하는지
- for loops : 반복문 진입하는지, 원하는 횟수만큼 실행되는지
- while loops : 종료조건이 제대로 동작하는지
- function : 호출, 파라미터, 결과



### 해결

- print 함수 활용
- 개발 환경 기능 활용
- Python tutor 활용
- 뇌컴파일, 눈디버깅



# 문법 에러

- Invalid syntax : 유효하지 않은 문법
- assign to literal : 값에 오류
- EOL, EOF : 괄호 오류



# 예외

- 문법적으로 올바르더라도 발생하는 에러
- ZeroDivisionError : 0으로 나눴을 때의 에러
- NameError : 변수 선언이 안 되어있는 경우
- TypeError
  - 타입 불일치 : 연산 불가능한 형태의 경우
  - argument 누락
  - argument 개수 초과
  - argument 타입 불일치
- ValueError : 타입은 올바르나 값이 적절하지 않은 경우
- IndexError : 인덱스가 존재하지 않거나 범위를 벗어나는 경우
- KeyError : 해당 키가 존재하지 않는 경우
- ModuleNotFoundError : 존재하지 않는 모듈을 import한 경우
- ImportError : 모듈은 있으나 가져온 클래스나 함수가 없을 경우
- KeyboardInterrupt : 임의로 프로그램 종료했을 때
- IndentationError : 들여쓰기가 적절하지 않을 때



# 예외 처리

- `try` : 실행
- `except` : 에러가 발생했을 때 실행
  - `except (a, b)` : 복수 예외처리
- `else` : 에러가 발생하지 않았다면 실행
- `Finally` : 최종정리문



# 예외 발생시키기

- raise : 실제 프로덕션 코드에서 활용
- assert : 예외 강제 발생, 디버깅용
  - 특정 조건이 False인 경우 발생