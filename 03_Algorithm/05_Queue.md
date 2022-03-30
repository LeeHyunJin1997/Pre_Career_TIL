# Queue

- 뒤에서 삽입, 앞에서 삭제하는 선입선출 구조
- FIFO (First In First Out)
- Front : 첫 번째 원소의 한 칸 앞, 공백의 인덱스
  - 최초 -1로 초기화
- Rear : 저장된 원소 중 마지막 원소의 인덱스
  - 최초 -1로 초기화



# 주요연산

- `enQueue(item)` : rear에 item을 삽입
- `deQueue()` : front 원소를 삭제 후 반환
- `createQueue(size)` : size 만큼의 공백의 큐를 생성
- `isEmpty()` : 큐가 공백인지 확인
  - 공백 : front == rear 인 상태
- `isFull()` : 큐가 포화인지 확인
  - 포화 : rear == size - 1
- `Qpeek()` : 검색, front를 삭제없이 반환

```python
def isEmpty():
    return front == rear


def isFull():
    return rear == len(Q) - 1


def enQueue(item):
    global rear
    if isFull():
        print("꽉 찼어")
    else:
        rear += 1
        Q[rear] = item


def deQueue():
    global front
    if isEmpty():
        print('비었어')
    else:
        front += 1
        return Q[front]


def Qpeek():
    if isEmpty():
        print('비었어')
    else:
        return Q[front+1]

    
# 큐를 의미대로 사용하기 위해선
# 미리 그 크기가 선언되어 있어야 함.
Q = [0] * 3
front = -1
rear = -1

# 1, 2, 3을 차례로 삽입하고 차례로 삭제
enQueue(1)
print(Q)
enQueue(2)
print(Q)
enQueue(3)
print(Q)
print(deQueue())
print(deQueue())
print(deQueue())
```

- 선형 큐의 문제: 삽입과 삭제를 반복할 경우, 앞부분이 비어있음에도 rear가 뒤로 밀려 포화상태로 인식
  - `.pop(0)`처럼 원소들을 한칸씩 당기는 방법을 사용할 수 있으나, 효율성이 급감
  - 원형 큐를 이용해 해결 가능





# 원형 큐

- 생김새는 그대로 1차원 배열이지만, 논리적으로 배열의 처음과 끝이 연결되어 있음을 가정
- 최초 공백상태는 front = rear = 0 으로 초기화
- `% n` 을 사용하여, n-1 이후에는 인덱스 0으로 순환
  - 삽입 위치 : (rear + 1) % n
  - 삭제 위치 : (front + 1) % n
- 공백과 포화를 모두 front == rear 로 진단

- 공백과 포화 상태를 구분하기 위해 front에는 원소를 두지 않음

  - 공백

    <img src="05_Queue.assets/image-20220330091433901.png" height="200px" width="200px" alt="image-20220330091433901"/>

  - 포화

    <img src="05_Queue.assets/image-20220330091613293.png" height="220px" width="230px" alt="image-20220330091613293"/>






# 우선순위 큐 (Priority Queue)

- 항목들이 우선순위를 가져, 우선순위가 높은 순서로 나가게 됨
- 삽입할 때 우선순위를 비교하여 적절한 위치에 삽입
- 가장 앞에 최고 우선순위 원소가 위치
- 삽입이나 삭제에 원소의 재배치가 일어나고, 소요되는 시간이나 메모리 낭비가 큼



# 버퍼 (Buffer)

- 데이터를 전송하는 공안 일시적으로 그 데이터를 보관하는 메모리
- 버퍼링 : 버퍼를 채우는 동작
- 순서대로 입력/출력/전달되어야 하므로 큐를 활용



# DEQ

- Queue의 양 끝에서 데이터의 삽입과 삭제 발생
- heap 사용