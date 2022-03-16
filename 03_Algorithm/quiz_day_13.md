https://swexpertacademy.com/main/learn/course/subjectDetail.do?courseId=AVuPDN86AAXw5UW6&subjectId=AWOVIoJqqfYDFAWg#

# 1. SWEA-5097

```python
# 회전
T = int(input())
for tc in range(1, T+1):
    # N 리스트 길이, M 이동 횟수
    N, M = map(int, input().split())
    lst = list(map(int, input().split()))
    rlt = lst[M % len(lst)]
    print(f'#{tc} {rlt}')
```



# 2. SWEA-5102

```python
# 노드의 거리
T = int(input())
for tc in range(1, T+1):
    # V 노드 개수, E 간선 개수
    V, E = map(int, input().split())
    links = [list(map(int, input().split())) for _ in range(E)]
    # S 출발 노드, G 도착노드
    S, G = map(int, input().split())
    # 노드 개수만큼의 빈 리스트
    lines = [list() for _ in range(V+1)]
    Q = [S]

    # lines 각 인덱스에 연결된 노드를 저장
    for i in links:
        lines[i[0]].append(i[1])
        lines[i[1]].append(i[0])

    cnt = -1
    end = False

    while True:
        if end:
            print(f'#{tc} {cnt}')
            break

        if not Q:
            print(f'#{tc} {0}')
            break

        for j in range(len(Q)):
            temp = Q.pop(0)

            if temp == G:
                end = True
                break

            for i in range(len(lines[temp])):
                Q.append(lines[temp][i])

            lines[temp] = []

        cnt += 1

```



# 3. SWEA-5105

```python
# 미로의거리
T = int(input())
for tc in range(1, 1+T):
    # N 미로크기
    N = int(input())
    arr = [list(map(int, input())) for _ in range(N)]

    # 출발지 도착지 찾기
    start = None
    end = None
    for r in range(N):
        for c in range(N):
            if arr[r][c] == 3:
                arr[r][c] = 0
                end = [r, c]
            elif arr[r][c] == 2:
                arr[r][c] = 1
                start = [r, c]

    queue = [start]
    # 상하좌우
    dr = [-1, 1, 0, 0]
    dc = [0, 0, -1, 1]

    cnt = -1
    finish = 0

    while True:
        # 도착지를 찾았을 경우
        if finish == 1:
            print(f'#{tc} {cnt}')
            break

        # 다 돌았는데 못 찾았을 경우
        if not queue:
            print(f'#{tc} 0')
            break

        for j in range(len(queue)):
            loc = queue.pop(0)

            for k in range(4):
                temp_r = loc[0] + dr[k]
                temp_c = loc[1] + dc[k]
                # 인덱스 에러 방지
                if temp_r < 0 or temp_r > N-1 or temp_c < 0 or temp_c > N-1:
                    continue
                elif [temp_r, temp_c] == end:
                    finish = 1
                    break
                else:
                    # 가려하는 곳이 안가본 통로라면
                    if arr[temp_r][temp_c] == 0:
                        arr[temp_r][temp_c] = 1
                        queue.append([temp_r, temp_c])

        # queue를 한번 비울 때마다 카운트
        cnt += 1
```



# 4. SWEA-5099

```python
# 피자굽기
def melt():
    fire.append(fire.pop(0))
    fire[0][1] = fire[0][1]//2

T = int(input())
for tc in range(1, T+1):
    # N 화덕크기, M 피자개수
    N, M = map(int, input().split())
    Cis = list(map(int, input().split()))
    pizza_lst = []

    # 피자리스트는 [피자번호, 치즈양] 형태
    for i in range(len(Cis)):
        pizza_lst.append([i+1, Cis[i]])

    # 최초 한바퀴
    fire = pizza_lst[0:N]
    pizza_lst = pizza_lst[N:]
    fire[0][1] = fire[0][1]//2


    while True:
        # 피자가 하나 남았을 때
        if len(fire) == 1:
            print(f'#{tc} {fire[0][0]}')
            break

        # 치즈가 다 녹았다면
        while fire[0][1] == 0:
            if len(fire) ==1:
                break
            # 새 피자가 없다면
            if not pizza_lst:
                # 다된 피자 빼고 뒷 피자도 녹았다!
                fire.pop(0)
                fire[0][1] = fire[0][1]//2
            # 새 피자 넣기
            else:
                fire[0] = pizza_lst.pop(0)

        melt()
```





# 5. SWEA-1226

https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV14vXUqAGMCFAYD

```python
# 미로 1
T = 10
for tc in range(1, T+1):
    N = int(input())
    arr = [list(map(int, input())) for _ in range(16)]

    visited = []
    stack = []

    # 상하좌우
    dr = [-1, 1, 0, 0]
    dc = [0, 0, -1, 1]

    for i in range(16):
        for j in range(16):
            if arr[i][j] == 2:
                start = [i, j]

    visited = []
    stack = [[start[0], start[1]]]
    goal = False

    while True:
        # 도착못할 경우
        if not stack:
            print(f'#{tc} {0}')
            break

        if goal:
            print(f'#{tc} {1}')
            break

        r = stack[-1][0]
        c = stack[-1][1]

        for k in range(4):
            temp_r = r + dr[k]
            temp_c = c + dc[k]
            # 도착지에 도착했을 경우
            if arr[temp_r][temp_c] == 3:
                goal = True
                break

            # 통로를 만날 경우 이동
            elif arr[temp_r][temp_c] == 0 and [temp_r, temp_c] not in visited:
                visited.append([temp_r, temp_c])
                stack.append([temp_r, temp_c])
                break

        # 사방이 막혀있을 경우
        else:
            stack.pop()
```

