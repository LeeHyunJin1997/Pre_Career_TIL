# 스택

- 자료를 쌓아올린 형태의 자료구조
- 후입 선출 구조 (LIFO, Last-In-First-Out)
- 용어
  - top : 마지막에 삽입된 원소의 위치
  - push : 삽입
  - pop : 꺼내기
- 연산
  - isEmpty : 스택이 공백인지 확인
  - peek : top에 있는 원소를 반환



# 재귀

- 자기 자신을 호출, 순환
- 특정 방식의 작업에서는 재귀를 사용한 함수가 훨씬 간단



# Memoization

- 재귀호출에서 엄청난 수의 중복호출이 발생하는 것을 막기위한 방법
- 이미 계산한 값은 저장한 후에, 불러오는 방식으로 진행
- 중복된 계산을 제거하여, 빠른 속도를 가짐
- 동적 계획법(DP)의 핵심



# Dynamic Programming

-  문제를 작은 부분들로 나누어, 작은 문제를 먼저 해결하고 그 결과로 보다 큰 문제를 해결하는 알고리즘

- Memoization을 사용하는 재귀적 구조보다 오버헤드가 작다
  - 오버헤드 : 어떤 작업을 처리하기 위해 드는 추가적인 시간이나 메모리



# DFS

- 깊이 우선 탐색
- 한 방향으로 깊이 나아가다가 진행할 수 없으면, 마지막 갈림길로 돌아가 다른 방향 탐색하는 것을 반복
  - 모든 경로를 추적
- 갈림길로 돌아가는 동작을 위해 스택을 사용
  - stack : 현재 경로를 담음. 더이상 진행할 수 없으면 하나씩 pop하며 진행할 수 있는 갈림길을 찾음
  - visited : 방문했던 지점들을 담음. 갈림길을 판단할 때 참고

```python
visited = []
stack = []
DFS(v)
	v 방문;
    visited[v] <- true;
    do {
        if (v의 인접 정점 중 방문 안한 w 찾기)
        	push(v);
        	while( w ){
                w 방문;
                visited[w] <- true;
                push(w);
                v<-w;
                v의 인접 정점 중 방문 안한 w 찾기
            }
        	v<-pop(stack);
    } while(v)
end DFS()
```



# 백트래킹

- 해를 찾는 도중에 막힐 경우, 그 경로를 포기하고 되돌아가 다시 해를 찾는 기법
- DFS와 유사하지만, 모든 경로를 추적하지 않고 가지치기를 해나가 시도 횟수가 비교적 적음



# 부분집합

- 2^n 개의 부분집합
- 백트래킹 기법으로 구할 수 있다

```python
# i 인덱스, N 원소 개수
def f(i, N):
    # 인덱스가 끝까지 오면 중단
    if i == N:
        # 비트(선택)에 해당하는 a의 원소 출력
        for j in range(N):
            if bit[j]:
                print(a[j], end = ' ')
   	else:
        # i번째 원소를 포함하고 진행
        bit[i] = 1
        f(i+1, N)
        # i번째 원소를 포함하지 않고 진행
        bit[i] = 0
		f(i+1, N)
    return


a = [1,2,3]
bit = [0,0,0]

f(0, 3)
```

- 부분집합의 합

```python
# i 인덱스, N 원소 개수, s 현재까지 선택된 원소 합, t 목표합
def f(i, N, s, t):
    # 부분집합의 합이 목표값일때
    if s == t:
        # 비트(선택)에 해당하는 a의 원소 출력
        for j in range(N):
            if bit[j]:
                print(a[j], end = ' ')
    # 더이상 고려할 원소가 없을 때
    elif i==N:
        return
    # 목표값을 지나쳤을 때
    elif s > t:
        return
   	else:
        # i번째 원소를 포함하고 진행
        bit[i] = 1
        f(i+1, N, s+a[i], t)
        # i번째 원소를 포함하지 않고 진행
        bit[i] = 0
		f(i+1, N, s, t)
    return


N = 10
a = [x for x in range(1, N+1)]
bit = [0] * N
# 합이 10인 부분집합을 찾기
t = 10

f(0, N, 0, t)
```



# 순열

```python
def f(i, N):
    # 끝까지 완성했을 경우 출력
    if i == N:
        print(p)
    else:
        for j in range(i, N):
            # 순서를 바꿔 진행
            p[i], p[j] = p[j], p[i]
            f(i+1, N)
            # 원래대로 복귀
            p[i], p[j] = p[j], p[i]
    
    
# 길이가 5인 순열
N = 5
p = [x for x in range(1, N+1)]
f(0, N)
```



# 분할 정복 알고리즘

- 분할 - 정복 - 통합
  - 문제를 작은 부분들로 나눠 각각 해결한 후, 해답을 모으는 방식

- 거듭제곱
  - C*C.. 와 같은 단순 거듭제곱은 계산량이 많음
  - C^8 = ((C^2)^2)^2 과 같은 개념으로 분할해 계산량을 줄일 수 있음

```python
# C 밑 n 지수
def Power(C, n):
    if n == 0 or C == 0:
        return 1
    # n이 짝수일 때
    if n % 2 == 0:
        new_C = Power(C, n/2)
        return new_C * new_C
    # n이 홀수일 때
    else:
        new_C = Power(C, (n-1)/2)
        return (new_C * new_C) * C
```

- 퀵 정렬
