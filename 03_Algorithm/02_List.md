# 배열

- 하나의 변수 선언으로 둘 이상의 값에 접근 가능



# 정렬

- 버블 정렬 (Bubble Sort)
  - 인접한 두 개의 원소를 비교해 자리 교환
  - 한 단계가 끝나면 가장 큰 원소가 마지막 자리로 이동
  - 시간 복잡도 O(n^2)

```python
def BubbleSort(a, N): 
    for i in range(N-1, 0, -1):
        for j in range(0, i):
            if a[j] >
```



- 카운팅 정렬 (Counting Sort)
  - 각 원소 숫자의 개수를 또 다른 리스트에 저장
  - 정수 자료에만 적용 가능 (일반적으로 자연수에 적용)
  - 비교적 n이 작을 때에만 가능
  - 시간 복잡도 O(n+K)

```python
def Counting_Sort(A, B, k)
# A [] -- 입력 배열 (1 to k)
# B [] -- 정렬된 배열
# C [] -- 카운트 배열

	C = [0] * (k+1)
    
    for i in range (0, len(A)):
        C[A[i]] += 1
        
    for i in range (1, len(C)):
        C[i] += C[i-1]
        
    for i in range (len(B)-1, -1, -1):
        C[A[i]] -= 1
        B[C[A[i]]] = A[i]
```



- 선택 정렬 (Selection Sort)

  - 가장 작은(큰) 값의 원소부터 차례대로 선택하여 위치 설정

  - 교환 횟수가 버블정렬, 삽입정렬보다 적다

  - O(n^2)

  - 셀렉션 알고리즘

    - k번째로 작은(큰) 원소를 찾는 알고리즘
    - k번째로 작은 원소까지 정렬시키고 k번째 원소를 반환

    

- 퀵 정렬 (Quick Sort)

- 삽입 정렬 (Insert Sort)

- 병합 정렬 (Merge Sort)



# 탐색법

- 완전 검색 (Exaustive Search)

  - 생각할 수 있는 모든 경우의 수를 나열

  - 수행속도는 느리지만, 해답을 찾지 못할 확률이 적다


- 탐욕(Greedy) 알고리즘

  - 여러 경우 중 각 순간에 최적인 것은 선택, 최종적인 해답에 도달한다.

  - 지역적으로는 최적이지만, 전역적으로 최적임을 보장할 수 없다.


  - 일반적으로 머릿속에 떠오르는 생각은 Greedy 접근법

  - 동작과정
    1) 해 선택 : 부분 최적해를 해 집합에 추가
    2) 실행가능성 검사 : 문제의 제약조건 위반 여부를 검사
    3) 해 검사 : 부분해 집합이 문제의 해가 되는지 검사




# 2차원 배열

- 행 우선 순회

```python
for i in range(n):
    for j in range(m):
        Array[i][j]
```



- 열 우선 순회

```python
for i in range(m):
    for j in range(n):
        Array[i][j]
```



- 지그재그 순회

```python
for i in range(n):
    for j in range(m):
        Array[i][j + (m-1-2*j) * (i%2)]
```



- 델타를 이용한 사방 탐색

```python
arr # NxN
di = [0, 0, -1, 1] # 좌우상하
dj = [-1, 1, 0, 0]
for i in range(N-1):
	for j in range(N-1):
        for k in range(4):
            ni = i + di[k]
            nj = j + dj[k]
```



- 전치 행렬

```python
arr = [[1,2,3],[4,5,6],[7,8,9]]

for i in range(3):
    for j in range(3):
        if i < j:
            arr[i][j], arr[j][i] = arr[j][i], arr[i][j]
```



# 부분집합

- 비트를 이용해 간결하게 부분집합을 생성하는 방법

- 비트 연산자
  - `&` : 비트 단위로 AND 연산
    - `i & (1 << j)` : i의 j번째 비트가 1인지 검사
  - `|` : 비트 단위로 OR 연산
  - `^` : 두 값이 다를 때 True
  - `<<` : shift 연산자. 비트 열을 왼쪽으로 이동
    - `1 << n` : 2^n, 원소가 n개일 때 부분집합의 수
  - `>>` : shift 연산자. 비트 열을 오른쪽으로 이동

```python
arr = [3, 6, 7, 1, 5, 4]

n= len(arr)

for i in range(1<<n):		# 1<<n : 부분 집합의 개수
    for j in range(n):		# 원소의 수만큼 비트를 비교
        if i & (1<<j):		# i의 j번 비트가 1인 경우
            print(arr[j], end=", ")
```



# 검색

- 목적하는 탐색 키를 가진 항목을 찾는 것

- 검색의 종류

  - 순차 검색

    - 일렬로 되어 있는 자료를 순서대로 검색
    - 검색 대상이 많을 경우 수행시간이 급증
    - 마지막까지 검색대상을 찾지 못하면 실패
    - 정렬되어 있지 않은 경우
      - 비교 횟수 : (n+1)/2
    - 정렬되어 있는 경우
      - 키 값이 검색대상보다 크면 검색 중지

  - 이진 검색

    ```python
    def binarySearch(a, N, key):
        start = 0
        end = N-1
        while start <= end:
            middle = (start + end) // 2
            if a[middle] == key:	# 검색 성공
                return True
            elif a[middle] > key:
                end = middle - 1
            else:
                start = middle + 1
        return false
    ```

    - 자료의 가운데 있는 항목의 키 값과 비교
    - 다음 검색의 위치 설정, 검색 범위 반감
    - 전제 : 자료가 정렬된 상태
      - 자료의 삽입이나 삭제가 발생했을 때, 정렬하는  추가 작업이 필요

  - 해쉬