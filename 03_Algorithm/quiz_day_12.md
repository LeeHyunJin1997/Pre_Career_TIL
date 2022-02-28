# 1.

```python
# 테스트케이스
T = int(input())
for tc in range(1, T+1):
    # N 행렬 크기
    N = int(input())
    arr = [list(map(int, input().split())) for _ in range(N)]

    # 상 하 좌 우
    dr = [-1, 1, 0, 0]
    dc = [0, 0, -1, 1]

    # 현재 경비원의 위치 특정
    # 벽의 개수 세기
    r = None
    c = None
    walls = 0
    for i in range(N):
        for j in range(N):
            if arr[i][j] == 2:
                r = i
                c = j
            elif arr[i][j] == 1:
                walls += 1

    # cnt 경비원의 감시가능 영역
    # 경비원이 서있는 자리(2) 포함
    cnt = 1
    # 각 방향으로
    for k in range(4):
        # m 나아가는 칸 수
        m = 1
        while True:
            temp_r = r + m * dr[k]
            temp_c = c + m * dc[k]
            # 인덱스 벗어날 경우 break
            if temp_r < 0 or temp_r > N-1 or temp_c < 0 or temp_c > N-1:
                break
            # 벽을 만날 경우 break
            elif arr[temp_r][temp_c] == 1:
                break
            # 그렇지 않으면 한칸 더 나아가기
            else:
                m += 1
                cnt += 1

    # 사각지대 = 전체 영역 - 감시 가능 영역 - 벽의 개수
    dark = N**2 - cnt - walls
    print(f'#{tc} {dark}')

```