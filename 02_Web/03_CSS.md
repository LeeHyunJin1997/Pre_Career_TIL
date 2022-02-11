# CSS

- **C**ascading **S**tyle **S**heets
- 선택하고 스타일을 지정한다.

```html
h1{
  color: blue;
  font-size: 15px;
}
```

- `h1`은 선택자
- 중괄호 안의 `font-size`는 속성, `15px`는 값
- 문장의 끝은 `;`로 마감
- 완성된 레이아웃 제공 : https://csslayout.io/



# CSS 정의 방법

- 인라인

```css
<h1 style="color: blue; font-size: 170px;">Hello CSS</h1>
```

- 내부 참조(embedding)

```html
<head>
  <style>
    h1{
      color: blue;
      font-size: 15px;
    }
  </style>
</head>
```

- **외부 참조(link file)**

  - 분리된 .CSS 파일을 생성

  - 코드의 재사용성이 높고, 유지보수가 쉬움

```html
<head>
  <link rel="Stlyesheet" href="style.css">
</head>
```

- 만약, 스타일 코드에 취소선이 생긴다면, 더 상위 요소에 의해 덮어씌워진 것



# 개발자도구

- styles : 해당 요소에 선언된 모든 CSS
- computed : 해당 요소에 최종 계산된 CSS



# 선택자 유형

- **기본 선택자**
  - `*` :전체 선택자
  - `h1` : 요소 선택자
    - 태그를 직접 선택
  - `.` : 클래스 선택자
    - 해당 클래스가 적용된 항목을 선택
  - `#` : 아이디 선택자
    - 해당 아이디로 정의된 요소를 선택
    - 일반적으로 한 아이디는 하나의 문서에 1번만 사용
  - 속성 선택자
- **결합자 (Combinators)**
  - 특정 조건을 만족하는 태그에 스타일을 적용
  - 자손 결합자
    - `A B` : A의 자손 중 B를 만족하는 태그를 선택
      - 자손 : 하위의 하위까지 포함
  - 자식 결합자
    - `A > B` : A의 자식 중 B를 만족하는 태그를 선택
  - 일반 형제 결합자
    - `A ~ B` : A의 형제 요소 중 뒤에 위치하는 B를 모두 선택
  - 인접 형제 결합자
    - `A + B` : A의 바로 다음에 오는 형제 요소  B 선택
- **의사 클래스/요소 (Pseudo Class)**
  - 특정 상태(동작)인 태그를 선택
    - 예 : `A:hover`, A 위에 마우스가 올라간 상태
  - 링크, 동적 의사 클래스
  - 구조적 의사 클래스, 기타 의사 클래스, 의사 엘리먼트, 속성 선택자



# CSS 적용 우선순위

- 인라인 > id > class, 속성, pseudo-class > 요소
  - class가 중첩된 경우, CSS에서 마지막으로 작성된 것이 적용 (덮어 씌워짐)




# CSS 상속

- 상속되는 속성
  - Text 요소, opacity
- 상속되지 않는 속성
  - Box model 관련 요소
  - position 관련 요소

- `inherit`을 이용해 상속되지 않는 것도 상속시킬 수 있음 
