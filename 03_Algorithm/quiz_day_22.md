# 1. 연습문제-DFS

```python
# 연습문제 1

# n 현재 정점
def DFS(n):
    # 방문한 정점이라면 그만
    if visited[n]:
        return

    # 처음 온거라면
    print(n, end=' ')
    visited[n] = 1

    # 해당 정점에 연결된 정점 수만큼 반복
    for i in range(len(edges[n])):
        DFS(edges[n][i])


# 정점개수
V = 7
lst = [1, 2, 1, 3, 2, 4, 2, 5, 4, 6, 5, 6, 6, 7, 3, 7]

# edges 각 정점(인덱스)에 연결된 정점들의 번호 저장
edges = [[] for _ in range(V+1)]
for j in range(0, len(lst), 2):
    edges[lst[j]].append(lst[j+1])
    edges[lst[j+1]].append(lst[j])

visited = [0] * (V+1)

start = 1

DFS(start)
print()
```



# 2. 연습문제-BFS

```python
# 연습문제 2

# 정점개수
V = 7
lst = [1, 2, 1, 3, 2, 4, 2, 5, 4, 6, 5, 6, 6, 7, 3, 7]

# edges 각 정점(인덱스)에 연결된 정점들의 번호 저장
edges = [[] for _ in range(V+1)]
for j in range(0, len(lst), 2):
    edges[lst[j]].append(lst[j+1])
    edges[lst[j+1]].append(lst[j])

visited = [0] * (V+1)

start = 1
queue = [start]

# queue가 빌 때까지
while queue:
    now = queue.pop(0)

    # 안 왔던 정점이라면
    if not visited[now]:
        print(now, end=' ')
        visited[now] = 1
        for i in edges[now]:
            queue.append(i)

print()
```



# 3. SWEA-5247

```python
# 연산
from collections import deque

T = int(input())
for tc in range(1, T+1):
    N, M = map(int, input().split())

    visited = set()
    queue = deque()
    queue.append(N)
    cnt = 0
    fin = 0

    while queue:
        for _ in range(len(queue)):
            temp = queue.popleft()

            # 백만이하의 자연수가 아니라면 넘어가
            if temp < 1 or 1000000 < temp:
                continue

            # 정답이라면
            if temp == M:
                fin = 1
                break

            # 연산을 계속 해야 한다면
            if temp not in visited:
                visited.add(temp)
                queue.append(temp-1)
                queue.append(temp-10)
                queue.append(temp+1)
                queue.append(temp*2)

        if fin:
            break

        cnt += 1

    print(f'#{tc} {cnt}')
```

- 제한시간 초과하는 테스트케이스가 존재
- 최대한 가지치기해야하며, 시간을 줄이기 위해 set과 deque 사용