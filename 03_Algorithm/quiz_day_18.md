# 1. SWEA-1952

https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV5PpFQaAQMDFAUq

```python
# 수영장

# n 월수(종료조건), ssum 비용합
def DFS(n, ssum):
    global min_val
    # 종료조건 (12개월)
    if n > 12:
        # 종료되었을 때 최솟값 갱신
        if min_val > ssum:
            min_val = ssum
        return

    DFS(n+1, ssum+lst[n]*day)   # 일일권: 한달 증가, +일수*일일권 가격
    DFS(n+1, ssum+mon)          # 월간: 한달 증가, + 1달권 가격
    DFS(n+3, ssum+mon3)         # 3달: 3달 증가, + 3달권 가격
    DFS(n+12, ssum+year)        # 년간: 12달 증가, +1년권 가격

T = int(input())
for tc in range(1, 1+T):
    day, mon, mon3, year = map(int, input().split())
    # 월별 이용계획, 인덱스와 월 맞춰줌
    lst = [0] + list(map(int, input().split()))
    min_val = 12345678

    DFS(1, 0)
    print(f'#{tc} {min_val}')
```



# 2. SWEA-2105

https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV5VwAr6APYDFAWu

```python
# 디저트 카페

# n 회전 횟수, ci, cj 현위치, visited 지나친 좌표, cnt 먹은 디저트 종류
def DFS(n, ci, cj, visited, cnt):
    global si, sj, max_val
    # 방향회전 2번했는데 최대치 반도 못 먹었으면 의미없어!
    if n==2 and max_val>=cnt*2:
        return
    # 방향회전을 4회했을 때 종료(의미 없음)
    if n > 3:
        return
    # 시작점으로 돌아왔고, 현재 정답보다 많이 먹었을 때
    if n == 3 and ci==si and cj==sj and max_val<cnt:
        max_val = cnt
        return

    # 직진(k=n) 혹은 방향 전환(k=n+1)
    for k in range(n, n+2):
        ni, nj = ci+di[k], cj+dj[k]
        # 배열의 범위 내인지, 중복 인지 체크
        if 0<=ni<N and 0<=nj<N and arr[ni][nj] not in visited:
            visited.append(arr[ni][nj])
            DFS(k, ni, nj, visited, cnt+1)
            visited.pop()


T = int(input())
for tc in range(1, T+1):
    N = int(input())
    arr = [list(map(int, input().split())) for _ in range(N)]
    # 정답 저장, 정답이 없을땐 -1
    max_val = -1
    # 대각선으로 움직이는 방향
    # k + 1 이 되어 인덱스 에러가 나는 것을 방지하기 위해 의미없는 5번째 값 삽입
    di, dj = (1,1,-1,-1,0),(-1,1,1,-1,0)

    # i, j에서 시작
    for si in range(0, N-2):
        for sj in range(1, N-1):
            DFS(0, si, sj, [], 0)

    print(f'#{tc} {max_val}')
```



# 3. SWEA-2819

https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV7I5fgqEogDFAXB

```python
# 격자판의 숫자 이어붙이기

# n 선택한 숫자 개수, ci, cj 현시점 좌표, num 만들어낸 숫자
def DFS(n, ci, cj, num):
    # 숫자 7개 채우면 종료
    if n == 7:
        sset.add(num)
        return
    # 상하좌우 네 방향 만들기
    for di,dj in ((-1,0),(1,0),(0,-1),(0,1)):
        ni, nj = ci+di, cj+dj
        # 이동할 방향이 격자 범위 내라면
        if 0<=ni<4 and 0<=nj<4:
            DFS(n+1, ni, nj, num*10+arr[ni][nj])


T = int(input())
for tc in range(1, T+1):
    arr = [list(map(int, input().split())) for _ in range(4)]
    # 경우의 수 중복제거를 위한 sset
    sset =set()
    for i in range(4):
        for j in range(4):
            DFS(0, i, j, 0)

    print(f'#{tc} {len(sset)}')
```



# 4. SWEA-4366

https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AWMeRLz6kC0DFAXd

```python
# 정식이의 은행업무
def solve(lst3):
    for i in range(len(lst2)):
        # 각 자리에서 1->0, 0->1 
        lst2[i] = (lst2[i]+1) % 2

        # 10진수로 변환
        dec = 0
        for idx in range(len(lst2)):
            dec = dec*2 + lst2[idx]

        # 3진수로 변환
        s = []
        ret = dec 
        while dec > 0:
            s.append(dec%3)
            dec //= 3
        lst = lst3[::-1]

        cnt = 0
        for idx in range(min(len(s), len(lst))):
            if s[idx] != lst[idx]:
                cnt += 1
        # 길이가 다른만큼도 체크
        cnt += abs(len(s)-len(lst))

        if cnt == 1:
            return ret

        # 원래대로 복구
        lst2[i] = (lst2[i]+1) % 2 


T = int(input())
for tc in range(1, 1+T):
    lst2 = list(map(int, input()))
    lst3 = list(map(int, input()))

    ans = solve(lst3)
    print(f'#{tc} {ans}')
```



# 5. SWEA-4615

https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AWQmA4uK8ygDFAXj

```python
# 재미있는 오셀로 게임

T = int(input())
for tc in range(1, 1+T):
    N, M = map(int, input().split())
    arr = [[0]*(N+1) for _ in range(N+1)]
    # 초기 톨 세팅
    arr[N//2][N//2] = arr[N//2+1][N//2+1] = 2
    arr[N//2+1][N//2] = arr[N//2][N//2+1] = 1

    for _ in range(M):
        sj, si, d = map(int, input().split())
        arr[si][sj] = d
        # 8방향으로
        for di, dj in ((-1,-1),(-1,0),(-1,1),(1,-1),(1,0),(1,1),(0,-1),(0,1)):
            s = []
            # 쭉 나아가면 확인
            for k in range(1, N):
                ni, nj = si+di*k, sj+dj*k
                # 범위 체크
                if 1<=ni<=N and 1<=nj<=N:
                    # 0 나오면 안봐도돼
                    if arr[ni][nj] == 0:
                        break
                    # 같은 돌인 때는
                    elif arr[ni][nj] == d:
                        # 뒤집어!
                        for ci,cj in s:
                            arr[ci][cj] = d
                        break
                    # 다른 돌이면 적어놔
                    else:
                        s.append((ni,nj))
                    
                else:
                    break
    
    # 개수 세기
    bcnt = wcnt = 0
    for lst in arr:
        bcnt += lst.count(1)
        wcnt += lst.count(2)

    print(f'#{tc} {bcnt} {wcnt}')
```



# 6. SWEA-2382

https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV597vbqAH0DFAVl

```python
# 미생물 격리
T = int(input())
di, dj = (0,-1,1,0,0),(0, 0, 0, -1, 1)
opp = [0,2,1,4,3]
for tc in range(1, 1+T):
    # N 배열 크기, M 시간, K 군집개수
    N, M, K = map(int, input().split())
    arr = [list(map(int, input().split())) for _ in range(K)]

    # M 시간 경과
    for _ in range(M):
        # 각각의 미생물 이동, 경계 처리
        for i in range(len(arr)):
            arr[i][0] = arr[i][0] + di[arr[i][3]]
            arr[i][1] = arr[i][1] + dj[arr[i][3]]
            # 경계값일 경우
            if arr[i][0] == 0 or arr[i][0] == N-1 or arr[i][1] == 0 or arr[i][1] == N-1:
                # 미생물 수 반으로 줄이고
                arr[i][2] //= 2
                # 방향은 반대로 바꿔줘
                arr[i][3] = opp[arr[i][3]]

        # 내림차순 정렬
        arr.sort(key=lambda x: (x[0],x[1],x[2]), reverse=True)

        # 좌표가 같은 경루 큰 미생물로 합치기
        i = 1
        while i < len(arr):
            if arr[i-1][0] == arr[i][0] and arr[i-1][1] == arr[i][1]:
                arr[i-1][2] += arr[i][2]
                arr.pop(i)
            else:
                i += 1
    
    ans = 0
    for i in range(len(arr)):
        ans += arr[i][2]

    print(f'#{tc} {ans}')
```



# 7. SWEA-2117

https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV5V61LqAf8DFAWu

```python
# 홈방법 서비스
T = int(input())
for tc in range(1, T+1):
    # N 도시 크기, M 각 집이 내는 비용
    N, M = map(int, input().split())
    arr = [list(map(int, input().split())) for _ in range(N)]

    # 각 집들의 좌표를 저장
    houses = []
    for i in range(N):
        for j in range(N):
            if arr[i][j] == 1:
                houses.append((i,j))

    max_val = 0
    # 각 좌표에서 집들과의 거리를 구해
    for ci in range(N):
        for cj in range(N):
            houses_dis = []
            for i in range(len(houses)):
                houses_dis.append(abs(houses[i][0]-ci) + abs(houses[i][1]-cj))

            # k 범위는 1 ~ N+1
            for k in range(1, N+2):
                cost = k*k + (k-1)*(k-1)
                cnt = 0
                # 거리가 k 미만인 집들의 수를 세
                for j in range(len(houses_dis)):
                    if houses_dis[j] < k:
                        cnt += 1
                
                # 해당 k에서 손해를 보지 않으면서 이전보다 더 많은 집에 서비스 제공할때
                if cnt*M >= cost and max_val < cnt:
                    max_val = cnt


    print(f'#{tc} {max_val}')
```

