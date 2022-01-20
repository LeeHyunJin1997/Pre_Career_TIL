# JSON

- Java Script Object Notation
- name(key) - value 형식

```python
{
    "firstName" : "Kwon"
    "lastName" : "YongJae"
}
```

- `open(<파일 경로>.<모드>,encoding)` 함수로 파이썬에서 실행 가능
  - 모드는 쓰기(`'w'`), 읽기(`'r'`), 수정(`'a'`)가 있음
  - `open()`은 `close()`와 한 쌍, 열었으면 닫아줘야 함
  - `with open() as <name>:` 으로 한시적으로 파일을 가져올 수 있음. 자동으로 `close()`