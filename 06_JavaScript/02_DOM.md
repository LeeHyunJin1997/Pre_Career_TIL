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
- `document.querySelectorAll(selector)` : 선택자에 해당하는 element들을 `NodeList`로 반환
  - `HTMLCollection` : name, id, index로 항목에 접근 가능
  - `NodeList` : index로만 항목에 접근 가능, 다양한 메서드 사용 가능


> getElementById, getElementByTagName, getElementByClassName 도 있지만, querySelector가 요소를 보다 구체적이고 유연하게 선택 가능



#### Collection

- Live Collection : DOM이 바뀔 때 실시간 업데이트
  - HTMLCollection, NodeList
- Static Collection : DOM이 변경되어도 collection 내용에는 영향을 주지 않음
  - `querySelectorAll()`의 반환 NodeList만 static



### 2. 변경 (Manipulation)

#### 메서드

- `document.createElement()` : 작성한 태그명의 HTML 요소를 반환
- `Element.append()` : 해당 Element의 마지막 자식으로 Node 객체나 문자열 삽입, 여러개 동시 삽입 가능, 반환값 없음
- `Node.appendChild()` : 해당 Node의 마지막 자식으로 삽입, Node만 삽입 가능, 하나씩만 삽입 가능, 삽입된 Node 반환
- `Node.remove()` : Node가 속한 트리에서 해당 Node를 제거
- `ParentNode.removeChild(ChildNode)` : ParentNode의 자식 ChildNode를 제거하고, 제거된 Node를 반환
- `Element.setAttribute(name, value)` : 해당 요소의 name 속성값을 value로 변경, 없는 속성이라면 추가
- `Element.getAttribute(attributeName)` : 해당 요소의 해당 속성의 속성값을 반환



#### 속성

- `Node.innerText` : 해당 요소 내부의 텍스트 컨텐츠를 반환
- `Element.innerHTML` : 해당 요소의 HTML 마크업을 반환
  - 공격자가 악성 스크립트를 직접 삽입할 수 있으므로 주의 (XSS 공격)



p.56.....