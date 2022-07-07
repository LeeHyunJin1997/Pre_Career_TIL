# JSX

javascript를 확장한 문법

HTML과 유사한 문법으로 엘리먼트를 생성할 수 있음

```react
// 기존 createElement를 이용해 h3 엘리먼트를 생성하는법
const h3 = React.createElement(
  "h3", 
  {
    id: "title",
    onMouseEnter: () => console.log("mouse enter"),
  },
  "Hello I'm a title");
```

```jsx
// jsx를 이용해 h3 엘리먼트를 생성하는 법
// HTML과 같은 직관적인 형태로 작성
const h3 = (
  <h3 id="title" onMouseEnter={() => console.log("mouse enter")}>
  Hello I'm a title
  </h3>
);
```



# babel/standalone

JSX로 작성된 엘리먼트를 javascript로 변환해 주기 위한 컴파일러

- JSX는 브라우저가 온전히 이해하지 못하기 때문에 컴파일러를 사용하지 않으면 에러가 난다.
- 다른 방식에 비해 느리다.

