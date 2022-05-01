# JavaScript

> 브라우저 화면을 동적으로 조작



### 브라우저 조작

- **D**ocument **O**bject **M**odel 조작
  - DOM : 문서를 트리 형태로 구조화
  - 문서(Document)가 객체로 구조화되어 있으며 Key로 접근 가능
  - 파싱(Parsing) : 브라우저가 문자열을 해석하여 DEM Tree로 만드는 과정
- **B**rowser **O**bject **M**odel 조작
  - 브라우저의 창(window)을 추상화해서 프로그래밍적으로 제어
- JavaScript Core
  - BOM과 DOM을 조작하기 위한 언어
  - ECMAScript 표준



### 스타일 가이드

> 자바스크립트는 세미콜론(`;`)을 선택적으로 사용 가능 (없으면 자동 삽입)

- Airbnb Javascript Style Guide
- Google Javascript Style Guide
- standardjs



<br>

---

<br>



# 변수

### 변수명 (식별자)

> 반드시 문자, `$`, `_`로 시작
>
> 대소문자를 구별
>
> 클래스명을 제외하고는 소문자로 시작
>
> 예약어 사용 불가

- `camelCase`: 변수, 객체, 함수에 사용
- `PascalCase`: 클래스, 생성자에 사용
- `SNAKE_CASE`: API_KEY와 같이 변경될 일 없는 상수값에 사용



### 변수 선언 키워드

- `let`
  - 재할당 가능
  - 재선언 불가능
  - 블록 스코프
- `const`
  - 재할당 불가능
  - 재선언 불가능
  - 블록 스코프
- `var`
  - 재할당 가능
  - 재선언 가능
  - 함수 스코프
  - 호이스팅 (변수 선언 전에도 `undefined`로 메모리 공간이 미리 할당)



<br>

---

<br>



# 데이터 타입

### 원시타입 (Primitive type)

> 객체가 아닌 타입
>
> 변수에 값이 담김
>
> 복사할 때 실제 값이 복사됨

- Number
  - 정수, 실수 구분 없는 부동소수점 형식
  - 계산이 불가능한 경우, `NaN` 반환
- String
  - 16비트 유니코드의 텍스트
  - `'`와 `"` 모두 사용 가능
  - backtick 사이에 `${ 변수명 }`를 사용해 표현식 삽입 가능 (ES6부터 지원)
- Boolean
  - `true` 혹은 `false`
  - `undefined`와 `null`은 항상 `false`
  - Object는 항상 `true`
  - Number는 `0`이나 `-0`, `NaN`일 경우, String은 빈 문자열일 경우 `false`
- undefined
  - 값이 없음을 나타냄
  - 변수 선언 후 값을 할당하지 않을 경우, 자동으로 `undefined` 할당
- null
  - "없는 값"임을 의도적으로 표현
  - EMCA 표준에 의해 원시타입에 속하지만, `typeof` 연산자 결과는 Object로 나타남



### 참조타입 (Reference type)

> 객체 타입
>
> 변수에 객체의 참조값이 담김
>
> 복사될 때 해당 참조값이 복사

- Function
- Array
- Object



<br>

---

<br>



# 연산자

### 할당 연산자

> 우변의 연산 결과를 좌변에 할당하는 연산자 

- `+=`
- `-=`
- `*=`
- `/=`
- `++` : 피연산자의 값을 1 증가시킴
- `--` : 피연산자의 값을 1 감소시킴



### 비교 연산자

> 피연산자들을 비교해 boolean 반환

- `<`
- `>`
- `==` : 피연산자를 암묵적으로 타입 변환해 값을 비교
- `===` : 타입 변환을 하지 않는 엄격한 비교, 타입과 값이 모두 같은지 확인



### 논리 연산자

> 단축 평가를 지원한다

- `&&` : and
- `||` : or
- `!` : not



### 삼항 연산자

> 조건식이 참이면 `:` 앞의 값을 사용, 그렇지 않으면 뒤의 값을 사용

```js
// example
const result = Math.PI > 4 ? 'Yes' : 'No'
console.log(reqult) //No
```



<br>

---

<br>



# 조건문

### if

> 소괄호`()`에 조건 작성
>
> 중괄호`{}`에 실행할 내용 작성
>
> 블록 스코프 생성

```js
if (condition) {
    // do something
} else if (condition) {
    // do something
} else {
    // do something
}
```



### switch

> 표현식과 case문의 값을 비교
>
> case에 해당하면 break를 만나거나 default문을 실행할 때까지 다음 조건문 실행
>
> 블록 스코프 생성

```js
switch(expression) {
  case 'A': {
    // expression === 'A'일 때 실행할 내용
    break // break가 없다면 다음 break까지 이어 실행
  }
  case 'B': {
    // expression === 'B'일 때 실행할 내용
    break
  }
  default: {
    // 어떤 case에도 해당하지 않을 때 실행
  }
}
```



<br>

---

<br> 

# 반복문

