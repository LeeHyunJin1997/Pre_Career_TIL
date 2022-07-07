# JSX

javascript를 확장한 문법

HTML과 유사한 문법으로 엘리먼트를 생성할 수 있음

```react
// 기존 javascript에서 h3 엘리먼트를 생성하는법
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
const h3 = (<h3 id="title" onMouseEnter={() => console.log("mouse enter")}>
  Hello I'm a title
  </h3>
);
```

