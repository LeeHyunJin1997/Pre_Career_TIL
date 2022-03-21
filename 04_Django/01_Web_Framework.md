# Static web page (정적 웹 페이지)

- 서버가 요청을 받은 경우 저장되어 있는 파일을 그대로 클라이언트에게 전달
- 모든 상황에서 모든 사용자에세 동일한 정보를 표시



# Dynamic web page (동적 웹 페이지)

- 서버가 요청을 받은 경우 추가적인 처리 과정을 거친 후 클라이언트에게 응답
- 상호작용을 하기 때문에 사용자마다 다른 웹페이지



# Framework

- 프로그래밍에서 특정 운영체제를 위한 표준구조와 이를 구현하는 클래스, 라이브러리 모임
- 재사용할 수 있는 코드를 프레임워크로 통합



# Django

- 검증된 Python 기반 Web framework
- 대규모 서비스에 안정적



# MVC Design Pattern

- model - view - controller
- 소프트웨어 공학에서 사용되는 디자인 패턴
- UI와 프로그램 로직을 분리하여 시각적인 요소의 이면의 부분을 영향 없이 고칠 수 있음
- 같은 모델을 Django에서는 MTV Pattern이라 부름



# MTV Pattern

- Model
  - 데이터 구조를 정의하고 데이터베이스의 기록을 관리
- Template
  - 파일 구조와 레이아웃 정의
  - 실제 내용을 보여줌
- View
  - HTTP 요청을 수신하고 응답을 반환
  - Model을 통해 필요한 데이터 접근
  - Template에게 응답의 서식 설정을 맡김


