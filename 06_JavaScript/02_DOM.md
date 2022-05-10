# DOM

> 문서를 구조화한 논리적 트리 모델
>
> 각각의 요소는 객체로 취급
>
> 최상위 객체 window
>
> window > document > html > ...



# DOM 조작하기

### 1. 선택 (Select)

- `document.querySelector(selector)` : 선택자에 해당하는 첫 element를 반환 (없다면 null)
- `document.querySelector(selector)` : 선택자에 해당하는 element들을 NodeList로 반환

> getElementById, getElementByTagName, getElementByClassName 도 있지만, querySelector가 요소를 보다 구체적이고 유연하게 선택 가능



### 2. 변경 (Manipulation)



p.35