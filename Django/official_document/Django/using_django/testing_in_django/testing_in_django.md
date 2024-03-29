# Testing in Django

테스트 자동화는 현대의 웹 개발자에게 정말 유용한 디버깅 툴이다. 여러 문제를 해결하고 예방하는데 테스트 묶음(**test suite**)을 사용할 수 있다:

- 새 코드를 작성할 때, 코드가 원한대로 동작하는지 검증하기 위해 테스트할 수 있다.
- 오래된 코드를 리팩토링하거나 수정할 때, 의도치 않게 앱의 동작이 변하는 것을 막을 수 있다.

웹앱은 HTTP 수준의 request 핸들링부터 form 유효성 검사와 처리 그리고 템플릿 렌더링까지, 여러 레이어의 로직으로 구성되어 있기 때문에, 웹앱을 테스트하는 것은 복잡한 일이다. Django의 테스트 실행 프레임워크와 다양한 유틸리티를 사용하면, request를 시뮬레이션하고, 테스트 데이터를 넣어보고, 앱의 output을 검사하고, 코드가 의도한대로 동작하는지 확인할 수 있다.

Django에서 권장하는 테스트 작성법은 Python 표준 라이브러리에 내장된 [unittest](https://docs.python.org/3/library/unittest.html#module-unittest) 모듈을 사용하는 것이다. 자세한 것은 [Writing and running tests](./writing_and_running_tests/writing_and_running_tests.md) 문서에서 다루고 있다.

 Django는 또 다른 Python 테스트 프레임워크와의 통합을 위해 API와 도구들을 제공한다. [Advanced testing topics]()의 [Using different testing framewoks]() 섹션에 설명되어 있다.

- [Writing and running tests](./writing_and_running_tests/writing_and_running_tests.md)
- [Testing tools]()
- [Advanced testing topics]()

