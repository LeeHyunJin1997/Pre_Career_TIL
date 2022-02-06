# 요청과 응답

- 클라이언트 : 요청하는 자
- 서버 : 응답하는 자

```python
import requests
from bs4 import BeautifulSoup

# 주소
url = 'https://finance.naver.com/sise/'
# 요청
response = requests.get(url)
# 응답된 객체에 저장되어 있는 것
print(response) # -> <Response [200]> / 200은 성공적 응답이라는 메시지
				# 에러의 경우 404(요청 오류), 500(응답 오류)
print(type(response)) # -> <class 'requests.models.Response'>
print(response.text) # -> str타입의 html을 보여줌


# BeautifulSoup 객체 -> HTML, XML을 조작하기 위함
data = BeautifulSoup(response.text, 'html.parser')
print(data) # -> response.text와 동일한 형태의 객체
print(type(data)) # -> <class 'bs4.BeautifulSoup'>, 타입이 바뀜
```



# API 활용

- 요청하는 방식에 대한 이해
  - 인증 방식
  - URL 생성
    - 기본 주소
    - 원하는 기능에 대한 추가 경로
    - 요청 변수
- 응답 결과에 대한 이해
  - 응답 결과 타입 (JSON)
  - 응답 결과 구조