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

### while

> 소괄호`()`에 조건문 작성
>
> 중괄호`{}`에 실행할 코드 작성

```js
let i = 0

while (i < 6) {
  console.log(i)
  i += 1
}
```



### for

> 초기화, 반복 조건, 실행부가 세미클론(`;`)으로 구분

```js
for (let i = 0; i < 6; i++) {
  console.log(i)
}
```



### for ... in

> 객체의 key를 순회
>
> 배열을 순회할 수 있지만 권장하지 않음

```js
const capitals = {
  korea: 'seoul',
  france: 'paris',
  USA: 'washington D.C.'
}

for (let capital in capitals) {
  console.log(capital);
}

// 출력: korea, france, USA
```



### for ... of

> 반복 가능한 객체의 값을 순회
>
> 대표적으로 배열 순회

```js
const fruits = ['딸기', '바나나', '메론']

for (let fruit of fruits) {
  fruit = fruit + '!'
  console.log(fruit) // 딸기!, 바나나!, 메론!
}

console.log(fruits); // ['딸기', '바나나', '메론']
```



<br>

---

<br>



# 함수

> 참조타입 중 하나로, function 타입
>
> 일급 객체(First-class citizen)에 해당
>
> - 변수에 할당 가능
> - 함수의 매개변수로 전달 가능
> - 함수의 반환 값으로 사용 가능



### 함수 선언식

> 함수의 이름과 함께 정의
>
> 함수명, 매개변수, 몸통부(중괄호) 존재
>
> 호이스팅이 발생해 선언 전에도 호출 가능, 정상 동작

```js
function add(num1, num2) {
  return num1 + num2 
}

// 함수 호출
add(1, 2)
```



### 함수 표현식

> 함수를 표현식 내에서 정의
>
> 함수명을 생략 가능(익명 함수)
>
> 함수 정의 전 호출 시 에러 발생

```js
const add = function (num1, num2) {
  return num1 + num2
}

add(1, 2)
```



### 매개변수

> 매개변수와 인자 개수의 불일치 허용
>
> 인자 개수가 많을 경우, 넘치는 부분은 버리고 매개변수로 사용
>
> 인자 개수가 적을 경우, 모자라는 인자는 `undefined`로 처리
>
> rest parameter(`...`)를 사용해 수가 정해지지 않은 매개변수를 지정, 배열로 받을 수 있음
>
> spread operator(`...`)를 이용, 배열을 전개해 인자로 전달 가능

```js
// 인자 개수가 많을 경우
const twoArgs = function (arg1, arg2) {
  return [arg1, arg2]
}

twoArgs(1, 2, 3) // [1, 2] 


// 인자 개수가 적을 경우
const threeArgs = function (arg1, arg2, arg3) {
  return [arg1, arg2, arg3]
}

threeArgs(1) // [1, undefined, undefined]
```

```js
// rest parameter
const restPar = function (arg1, arg2, ...restArgs) {
  return [arg1, arg2, restArgs]
}

console.log(restPar(1, 2, 3, 4, 5)) // [1, 2, [3, 4, 5]]
console.log(restPar(1, 2)) // [1, 2, []]

// spread operator
const spreadOpr = function (arg1, arg2, arg3) {
  return arg1 + arg2 + arg3
}

const numbers = [1, 2, 3]
console.log(spreadOpr(...numbers)) // 6
```



### Arrow Function

> 함수를 보다 간결하게 정의
>
> `function`, `()`, `{}` 생략 가능 

```js
const arrow1 = function (name) {
  return `hello, ${name}`
}

// 1. function 키워드 삭제
const arrow2 = (name) => { return `hello, ${name}` }

// 2. 매개변수가 1개일 경우, () 생략 가능
const arrow3 = name => { return `hello, ${name}` }

// 3. 중괄호 내부가 return문 하나일 경우 {}와 return 생략 가능
const arrow4 = name => `hello, ${name}`
```



<br>

---

<br>



# String

### 메서드

- `string.includes(value)` : string에 value의 존재 확인 후 boolean 반환
- `string.split(value)` : value를 기준으로 나눈 배열을 반환
  - value가 없을 경우 기존 문자열을 그대로 배열에 넣어 반환
  - value가 빈 문자열(`''`)일 경우 각 문자 단위로 나눈 배열 반환
- `string.replace(from, to)` : 가장 앞의 `from`을 `to`로 바꿔 반환
  - `string.replaceAll(from, to)` : 모든 `from`을 `to`로 바꿔 반환
- `string.trim()` : 문자열 앞뒤 공백문자(스페이스, 탭, 엔터) 제거
  - `string.trimStart()` : 문자열 앞 공백문자 제거
  - `string.trimEnd()` : 문자열 뒤 공백문자 제거



<br>

---

<br>



# Arrays

> 키와 속성을 담고 있는 참조 타입 객체
>
> 순서를 보장
>
> 음의 정수 접근 불가

```js
// length를 이용해 인덱스 뒤에서부터 접근하기
const numbers = [1, 2, 3, 4, 5]

console.log(numbers[numbers.length - 1]) // 5
```



### 메서드

- `array.reverse()` : 원본 배열을 거꾸로 정렬
- `array.push(item)` : 원본 배열 가장 뒤에 item 추가
- `array.pop()` : 원본 배열의 마지막 요소 제거
- `array.unshift(item)` : 원본 배열의 가장 앞에 item 추가
- `array.shift()` : 원본 배열의 첫번째 요소 제거
- `array.includes(value)` : 배열에 value가 존재하는지 판별한 후 boolean 반환
- `array.indexOf(value)` : 배열에 value가 존재한다면 먼저 찾은 인덱스를, 존재하지 않는다면 -1 반환
- `array.join(separator)` : 배열의 각 요소를 separator로 연결해 문자열 반환, 생략시 쉼표가 기본값



### 배열을 순회하며 콜백함수를 사용하는 메서드

> 콜백함수: 어떤 함수의 내부에서 실행될 목적으로 인자로 넘겨받는 함수
>
> 콜백함수의 매개변수: (element, index, array)
>
> 배열의 각 요소에 대해 콜백함수를 한번씩 실행

- `.forEach()`
  - 반환 값 없음

```js
const fruits = ['딸기', '수박', '사과', '체리']

fruits.forEach((fruit, index) => {
  console.log(fruit, index)
  // 딸기 0
  // 수박 1
  // 사과 2
  // 체리 3
})
```



- `.map()`
  - 콜백함수의 반환값들을 모아 새로운 배열 반환

```js
const numbers = [1, 2, 3, 4, 5]

const doubleNums = numbers.map((num) => {
  return num * 2
})

console.log(doublenums) // [2, 4, 6, 8, 10]
```



- `.filter()`
  - 반환값이 참인 요소를 모아 새로운 배열 반환

```js
const numbers = [1, 2, 3, 4, 5]
const oddNums = numbers.filter((num, index) => {
  return num % 2
})

console.log(oddNums) // 1, 3, 5
```



- `.reduce()`
  - 누적을 위한 콜백함수 내의 첫번째 매개변수 `acc`
  - 모든 콜백함수를 실행한 후 `acc` 반환
  - `reduce()`의 마지막 매개변수로 `acc`의 초기화를 위한 값 주어짐, 기본값은 기존 배열의 첫번째 값

```js
const numbers = [1, 2, 3]
const result = numbers.reduce((acc, num) => {
  return acc + num
}, 0)

console.log(result); // 6
```



- `.find()`
  - 반환값이 참인 첫번째 요소 반환
  - 찾는 값이 배열에 없으면 `undefined` 반환

```js
const avengers = [
  { name: 'Tony Stark', age: 45 },
  { name: 'Steve Rogers', age: 32 },
  { name: 'Thor', age: 40 },
]

const result = avengers.find((avengers) => {
  return avengers.name === 'Tony Stark'
})

console.log(result) // { name: 'Tony Stark', age: 45 }
```



- `.some()`
  - 요소 중 하나라도 주어진 판별함수가 참이라면 `true` 반환
  - 빈 배열은 항상 거짓 반환

```js
const numbers = [1, 3, 5, 7, 9]

const hasEvenNumber = numbers.some((num) => {
  return num % 2 === 0
})
console.log(hasEvenNumber) // false

const hasOddNumber = numbers.some((num) => {
  return num % 2
})
console.log(hasOddNumber) // true
```



- `.every()`
  - 모든 요소가 주어진 판별함수를 통과하면 `true` 반환
  - 빈 배열은 항상 `true` 반환

```js
const numbers = [2, 4, 6, 8, 10]

const isEveryNumberEven = numbers.every((num) => {
  return num % 2 === 0
})
console.log(isEveryNumberEven) // true

const isEveryNumberOdd = numbers.every((num) => {
  return num % 2
})
console.log(isEveryNumberOdd) // false
```



<br>

---

<br>



# Objects

> 객체는 속성(property)의 집합이며, 중괄호 내부에 key와 value 쌍으로 표현
>
> key는 문자열 타입
>
> value는 모든 타입 가능
>
> 객체의 요소는 점 또는 대괄호로 가능 (key에 띄어쓰기 같은 구분자가 있으면 대괄호로만 접근 가능)

```js
const me = {
  name: 'jack',
  phoneNumber: '01012345678',
  'samsung products': {
    buds: 'Galaxy Buds pro',
    galaxy: 'Galaxy s20',
  },
}

console.log(me.name);                       // jack
console.log(me.phoneNumber);                // 01012345678
console.log(me['samsung products']);        // {buds: 'Galaxy Buds pro', galaxy: 'Galaxy s20'}
console.log(me['samsung products'].buds);   // Galaxy Buds pro
```



### this

> 메서드 내에서 `this` 키워드는 해당 객체를 의미함

```js
const me = {
  firstName: 'John',
  lastName: 'Doe',
  fullName: this.firstName + this.lastName,

  getFullName: function () {
    return this.firstName + this.lastName
  }
}

console.log(me.firstName);        // John
console.log(me.lastName);         // Doe
console.log(me.fullName);         // fullName은 메서드가 아니기 때문에 정상 출력되지 않음 (NaN)
console.log(me.getFullName());    // JohnDoe
```



p.141
