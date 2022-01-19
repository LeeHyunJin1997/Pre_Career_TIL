# 모듈

- 특정 기능을 하는 코드
- 파이썬 파일 단위 (.py)
- `import` 로 모듈을 불러옴
  - `from` 과 함께 쓰이기도 함
  - `import *` 은 모듈 전체를 가져옴



## 패키지

- 여러 모듈의 집합
- 패키지에 `__init__.py`를 만들어야 패키지로 인식



## 파이썬 패키지 관리자(pip)

- PyPI에 저장된 외부 패키지들을 설치하도록 도와주는 명령어

```python
$ pip install SomePackage #$은 cmd에서 실행하라는 명령
$ pip install SomePackage==version #버전을 지정 가능
$ pip install 'SomePackage>=version'

$ pip uninstall SomePackage #설치된 패키지를 확인
$ pip list
$ pip show Somepackage

$ pip freeze > requrements.txt # 현재 버전을 텍스트 파일로 저장
```



## 가상환경



