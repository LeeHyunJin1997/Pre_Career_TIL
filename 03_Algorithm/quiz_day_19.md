# 1. SWEA-5188

https://swexpertacademy.com/main/learn/course/subjectDetail.do?courseId=AVuPDYSqAAbw5UW6&subjectId=AWUYDrI61lYDFAVT

```python
# 최소합

def move(n, m, s):
    """
    :param n: 우로 이동한 횟수
    :param m: 하로 이동한 횟수
    :param s: 현재까지의 부분 합
    :return:
    """
    global rlt
    # 진행중인 경로합이 이미 최솟값을 넘어갔다면
    if s > rlt:
        return

    # 오른쪽 아래로 정상적으로 이동했을 때
    if n == N-1 and m == N-1:
        rlt = s
        return

    # 배열을 넘어갔을 때
    if n > N-1:
        return

    if m > N-1:
        return

    # 우로 더이상 못갈때 하로만 진행
    if n == N-1:
        move(n, m+1, s+arr[n][m+1])

    # 하로 더이상 못갈때 우로만 진행
    elif m == N-1:
        move(n+1, m, s+arr[n+1][m])

    # 둘다 진행
    else:
        move(n+1, m, s+arr[n+1][m])
        move(n, m+1, s+arr[n][m+1])


T = int(input())
for tc in range(1, T+1):
    N = int(input())
    arr = [list(map(int, input().split())) for _ in range(N)]

    rlt = 999999999

    move(0, 0, arr[0][0])

    print(f'#{tc} {rlt}')
```



# 2. SWEA-5189

https://swexpertacademy.com/main/learn/course/subjectDetail.do?courseId=AVuPDYSqAAbw5UW6&subjectId=AWUYDrI61lYDFAVT

```python
# 전자카트

def f(i, N):
    """
    1로 끝나는 순열을 생성하는 함수
    :param i: 현위치
    :param N: 순열길이
    :return:
    """
    if i == N:
        routes.append(p + [1])
    else:
        for j in range(i, N):
            p[i], p[j] = p[j], p[i]
            f(i+1, N)
            # 원래대로 복구
            p[i], p[j] = p[j], p[i]


T = int(input())
for tc in range(1, T+1):
    # N 배열크기
    N = int(input())
    # e 배터리 소비량 표
    e = [list(map(int, input().split())) for _ in range(N)]

    p = [x for x in range(1, N+1)]

    routes = []

    # 양 끝이 1로 고정된 경로(순열)를 탐색
    f(1, N)

    # 각 경로 별로 배터리 소비량을 찾기
    min_battery = 999999999
    for i in range(len(routes)):
        battery = 0
        for j in range(1, N+1):
            battery += e[routes[i][j-1] - 1][routes[i][j] - 1]

        if battery < min_battery:
            min_battery = battery

    print(f'#{tc} {min_battery}')
```



# 3. SWEA-5201

https://swexpertacademy.com/main/learn/course/subjectDetail.do?courseId=AVuPDYSqAAbw5UW6&subjectId=AWUYEGw61n8DFAVT#

```python
# 컨테이너 운반

T = int(input())
for tc in range(1, T+1):
    # N 컨테이너 개수, M 트럭 개수
    N, M = map(int, input().split())
    # 컨테이너 무게 리스트
    w = list(map(int, input().split()))
    # 트럭 용량 리스트
    t = list(map(int, input().split()))

    # 가장 큰 트럭에도 못 들어가는 컨테이너는 날려버려
    w.sort()
    t.sort()

    rlt = 0
    while True:
        # 화물이나 트럭이 더이상 안 남았으면 그만
        if not w:
            break

        if not t:
            break

        # 가장 큰 트럭이 가장 큰 화물을 못 담는 다면 다음 화물
        if w[-1] > t[-1]:
            w.pop()
        # 담을 수 있다면 담아서 출발~
        else:
            rlt += w[-1]
            w.pop()
            t.pop()

    print(f'#{tc} {rlt}')

```



# 5. SWEA-5203

https://swexpertacademy.com/main/learn/course/subjectDetail.do?courseId=AVuPDYSqAAbw5UW6&subjectId=AWUYEGw61n8DFAVT#

```python
# 베이비진 게임

def check(player):
    count = [0] * 12
    for k in player:
        count[k] += 1

    # 9, 0, 1을 비교하기 위해 count 연장
    count[10], count[11] = count[0], count[1]

    for j in range(len(count) - 2):
        # 연이은 숫자가 1개 이상일 때
        if count[j] >= 1 and count[j + 1] >= 1 and count[j + 2] >= 1:
            return True
        # 한 숫자가 3개 이상일 때
        if count[j] >= 3:
            return True

    # 해당 하지 않으면
    else:
        return False


T = int(input())
for tc in range(1, T+1):
    cards = list(map(int, input().split()))
    # A 플레이어1 B 플레이어2
    A = []
    B = []

    rlt = 0
    for i in range(len(cards)):
        # 한장씩 나눠줘
        if i % 2:
            B.append(cards[i])
        else:
            A.append(cards[i])

        # 3장도 안 되면 카드 계속 받아
        if len(A) < 3 and len(B) < 3:
            continue

        # A만 먼저 3장을 받았을 때는 A만 체크
        if len(A) == 3 and len(B) == 2:
            if check(A):
                rlt = 1
                print(f'#{tc} {1}')
                break

        else:
            if check(A):
                rlt = 1
                print(f'#{tc} {1}')
                break

            if check(B):
                rlt = 1
                print(f'#{tc} {2}')
                break

    if rlt == 0:
        print(f'#{tc} {rlt}')
```

