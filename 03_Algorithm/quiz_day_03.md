# 연습문제 1.

- 5x5 행렬에서 (각 원소 - 상하좌우 원소)의 절댓값의 합을 구하라.

```python
num_list = []

for i in range(5):
    row = [j+5*i for j in range(1, 6)] # 한 줄로 반복된 원소를 가진 리스트를 생성하는 방식
    num_list.append(row)

# 변화량 값을 갖는 델타. 각각 상, 하, 좌, 우를 의미
dr = [-1, 1, 0, 0]
dc = [0, 0, -1, 1]
total = 0

# 행 선택
for r in range(len(num_list)):
    # 열 선택
    for c in range(len(num_list[0])):
        for k in range(4):
            each_row = r + dr[k]
            each_col = c + dc[k]

            # Index Error를 방지하기 위한 조건
            if each_row < 0 or each_row > 4 or each_col < 0 or each_col > 4:
                continue
            else:
                sub = num_list[r][c] - num_list[each_row][each_col]

                # 삼항연산자
                sub = sub if sub >= 0 else -sub
                total += sub

print(total)
```



# 연습문제 2.

- 입력된 리스트의 부분집합 중에서 원소들의 합이 0 인 부분집합이 있으면 1, 아니면 0을 출력하라.

```python
T = int(input())

for tc in range(1, T+1):
    num_list = list(map(int, input().split()))

    n = len(num_list)
    is_zero = 0

    for i in range(1 << n):     # 부분 집합의 개수(2^n) 만큼 반복
        sets = []               # 하나의 부분집합
        total = 0               # 원소들의 합

        for j in range(n):      # 원소의 수만큼 비트를 비교
            if i & (1 << j):    # i의 j번 비트가 1인 경우
                sets.append(num_list[j])

        if len(sets) == 0:      # sets가 공집합이면 넘어감
            continue

        else:
            for k in sets:      # 부분집합 원소들의 합
                total += k

            if total == 0:      # 합이 0인지를 판별, 조건에 걸리지 않는다면 0 (False)
                is_zero = 1

    print(f'#{tc} {is_zero}')
```



# SWEA 1954

https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV5PobmqAPoDFAUq

```python
T = int(input())

for tc in range(1, T+1):
    N = int(input())      # 달팽이 크기 N

    # NxN 크기 행렬 생성
    matrix = [[0]*N for _ in range(N)]

    # 델타 : 우하좌상
    dx = [0, 1, 0, -1]
    dy = [1, 0, -1, 0]

    # 시작 위치
    x = 0
    y = 0
    cnt = 1
    # 시작 방향은 오른쪽
    k = 0

    # 행렬의 원소 개수만큼 반복
    for _ in range(N*N):
        matrix[x][y] = cnt
        cnt += 1

        # 방향대로 한 칸 이동
        x, y = x + dx[k], y + dy[k]

        # x, y가 인덱스를 벗어나거나 이미 채워져 있으면
        if x < 0 or x > N-1 or y < 0 or y > N-1 or matrix[x][y]:
            # 이동 전 칸으로 돌아감
            x, y = x - dx[k], y - dy[k]
            # 방향 바꿔서
            k += 1
            if k > 3:
                k -= 4
            # 다시 이동
            x, y = x + dx[k], y + dy[k]

    print(f'#{tc}')
    for i in matrix:
        for j in i:
            print(j, end=' ')
        print('')

```



# SWEA 1209

https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV13_BWKACUCFAYh

```python
import sys
sys.stdin=open('input.txt')

for _ in range(10):
    tc = int(input())
    matrix = []
    sums = []

    for _ in range(100):
        matrix.append(list(map(int, input().split())))

    # 가로 합
    for i in range(len(matrix)):
        cnt = 0

        for j in range(len(matrix[0])):
            cnt += matrix[i][j]

        sums.append(cnt)

    # 세로 합
    for j in range(len(matrix[0])):
        cnt = 0

        for i in range(len(matrix)):
            cnt += matrix[i][j]

        sums.append(cnt)

    # 좌측상단에서 출발하는 대각선 합
    for i in range(len(matrix)):
        cnt = 0
        cnt += matrix[i][i]

    sums.append(cnt)

    # 우측상단에서 출발하는 대각선 합
    for i in range(len(matrix)):
        cnt = 0
        cnt += matrix[i][len(matrix)-1-i]

    sums.append(cnt)

    max_val = 0

    for i in sums:
        if max_val < i:
            max_val = i

    print(f'#{tc} {max_val}')

```

