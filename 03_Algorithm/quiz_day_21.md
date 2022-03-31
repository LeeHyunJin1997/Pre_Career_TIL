# 1. SWEA-5205

```python
# 퀵정렬
def quick_sort(low, high):
    # 더이상 바꿀게 없다면 return
    if high <= low:
        return

    mid = partition(low, high)
    # partition 을 기준으로 분할 정렬
    quick_sort(low, mid-1)
    quick_sort(mid+1, high)


def partition(low, high):
    pivot = (low + high) // 2
    L = low
    R = high
    while L < R:
        # 피봇보다 작은 값을 찾으며 L 이동
        while L < R and A[L] < A[pivot]:
            L += 1
        # 피봇보다 크거나 같은 값을 찾으며 R 이동
        while L < R and A[pivot] <= A[R]:
            R -= 1

        # L, R이 서로 만나지 않고 정지했을 때
        if L < R:
            # R, L 값 교환
            A[R], A[L] = A[L], A[R]
            # pivot 좌측에 더이상 큰 값이 없으면
            if L == pivot:
                # 피봇을 옮겨
                pivot = R

    # L == R일 때는 피봇과 R(L) 값 바꿔
    A[pivot], A[R] = A[R], A[pivot]
    return R


T = int(input())
for tc in range(1, T+1):
    N = int(input())
    A = list(map(int, input().split()))
    quick_sort(0, len(A)-1)
    print(f'#{tc} {A[N//2]}')

```



# 2. SWEA-5207

```python
# 이진 탐색

# l 시작 인덱스, r 끝 인덱스, num 찾는 숫자, select 좌우선택여부
def bin(l, r, num, select):
    m = (l + r) // 2

    # 값을 못 찾았을 경우
    if l == r and A[m] != num:
        return False

    # 값을 찾았을 경우
    if A[m] == num:
        return True
    # 찾는 값보다 작으면 오른쪽 구간 선택
    elif A[m] < num:
        # 이 전에도 오른쪽을 선택했으면 False
        if select == 1:
            return False
        else:
            return bin(m+1, r, num, 1)
    # 찾는 값보다 크면 왼쪽 구간 선택
    else:
        # 이 전에도 왼쪽을 선택했으면 False
        if select == -1:
            return False
        else:
            return bin(l, m-1, num, -1)


T = int(input())
for tc in range(1, T+1):
    N, M = map(int, input().split())
    A = sorted(list(map(int, input().split())))
    B = list(map(int, input().split()))
    cnt = 0

    # B에 있는 수를 탐색
    for i in B:
        if bin(0, N-1, i, 0):
            cnt += 1

    print(f'#{tc} {cnt}')
```



# 3. SWEA-5208

```python
# 전기버스2
# BFS 사용, 제한시간 조건 만족시키지 못해 실패

T = int(input())
for tc in range(1, T+1):
    lst = list(map(int, input().split()))
    # 정류장 수
    N = lst[0]

    queue = [1]
    cnt = 0
    fin = False

    while queue:
        for _ in range(len(queue)):
            now = queue.pop(0)

            # 현재 정류장에서 갈 수 있는 모든 정류장 추가
            for i in range(1, lst[now]+1):
                # 종점에 갈 수 있다면
                if now+i >= N:
                    fin = True
                    break
                queue.append(now+i)

            if fin:
                break

        if fin:
            break

        cnt += 1

    print(f'#{tc} {cnt}')
```



```python
# 전기버스2

# 정류장 n에 도착할 수 있는 가장 먼 정류장을 찾는 함수
def find(n):
    for i in range(n-1, 0, -1):
        if i + lst[i] >= n:
            first = i
    return first


T = int(input())
for tc in range(1, T+1):
    lst = list(map(int, input().split()))
    # 정류장 수
    N = lst[0]

    cnt = -1
    now = N
    while now > 1:
        now = find(now)
        cnt += 1

    print(f'#{tc} {cnt}')

```



# 4. SWEA-5209

```python
# 최소 생산 비용
def DFS(r, now_sum):
    global min_val
    # 끝 행에 도달하면 최솟갑을 갱신하고 리턴
    if r == N:
        if min_val > now_sum:
            min_val = now_sum
        return

    # 가지치기, 현재 합이 이미 최솟갑을 넘어서면 볼 필요없음
    if min_val < now_sum:
        return

    for c in range(N):
        # 선택 안한 열에 한해
        if not visited[c]:
            # 선택하고 다음 행 진행
            visited[c] = 1
            DFS(r+1, now_sum + arr[r][c])
            # 다음 열을 위해 원래대로 복구
            visited[c] = 0


T = int(input())
for tc in range(1, T+1):
    N = int(input())
    arr = [list(map(int, input().split())) for _ in range(N)]
    # 이미 사용한 줄을 체크
    visited = [0] * N

    min_val = 99999999

    DFS(0, 0)

    print(f'#{tc} {min_val}')
```



# 5. SWEA-1865

```python
# 동철이의 일 분배
def DFS(r, now_p):
    global max_p

    # 마지막 행까지 돌았을 때 최댓값 갱신
    if r == N:
        if now_p > max_p:
            max_p = now_p
        return

    # 다 돌지도 않았는데 벌써 값이 작다면 가지치기
    if max_p >= now_p:
        return

    for c in range(N):
        if not visited[c]:
            visited[c] = 1
            DFS(r+1, now_p * (arr[r][c]/100))
            visited[c] = 0


T = int(input())
for tc in range(1, T+1):
    N = int(input())
    arr = [list(map(int, input().split())) for _ in range(N)]
    visited = [0] * N
    max_p = 0

    DFS(0, 1)

    print(f'#{tc} {max_p*100:0.6f}')
```

