# Queue

- 뒤에서 삽입, 앞에서 삭제하는 선입선출 구조
- FIFO (First In First Out)
- Front : 저장된 원소 중 첫번째 원소의 인덱스
  - 최초 -1로 초기화
- Rear : 저장된 원소 중 마지막 원소의 인덱스
  - 최초 -1로 초기화
- enQueue : 삽입
- deQueue : 삭제



# 주요연산

- `enQueue(item)` : rear에 item을 삽입
- `deQueue()` : front 원소를 삭제 후 반환
- `createQueue(size)` : size 만큼의 공백의 큐를 생성
- `isEmpty()` : 큐가 공백인지 확인
  - 공백 : front == rear
- `isFull()` : 큐가 포화인지 확인
  - 포화 : rear == size - 1
- `Qpeek()` : front를 삭제없이 반환



# 원형 Queue

- 공백과 포화를 모두 front == rear 로 진단
- `%` 사용



- ~~공백과 포화 상태를 구분하기 위해 front에는 원소를 두지 않음~~



# DEQ

- Queue의 양 끝에서 데이터의 삽입과 삭제 발생
- heap 사용