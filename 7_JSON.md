# JSON

- Java Script Object Notation
- name(key) - value 형식

```python
{
    "firstName" : "Kwon"
    "lastName" : "YongJae"
}
```

- `open(<파일 경로>, mode='r', encoding=None)` 함수로 파이썬에서 실행 가능
  - 모드는 쓰기(`'w'`), 읽기(`'r'`), 수정(`'a'`)가 있음
  - `open()`은 `close()`로 종료시켜주지 않으면 오류가 남
  - `with open() as <name>:` 으로 한시적으로 파일을 가져올 수 있음. 자동으로 `close()`

- `json.dumps(x)`: 리스트를 json 형식으로 변환
- `x = json.load(f)` : json을 불러와 객체로 저장
- `pprint`를 이용해 더 깔끔하게 출력 가능