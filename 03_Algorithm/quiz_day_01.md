# 1. Gravity

```python
T = int(input())

for tc in range(1, T+1):
    # 테스트 케이스의 길이
    N = int(input())
    # 상자 배치
    boxes = list(map(int, input().split()))
    cnt_list = []

    # 낙차 = 나와 벽의 거리 - 그 사이에 있는 상자 수
    for i in range(len(boxes)):
        cnt = len(boxes) - i - 1
        # 자신보다 우측에 있는 상자 스택 중 더 높거나 같은 것을 탐색
        for j in range(i+1, len(boxes)):
            if boxes[i] <= boxes[j]:
                cnt -= 1
        cnt_list.append(cnt)

    # cnt_list 에서 최대 낙차를 구함
    rlt = 0
    for i in cnt_list:
        if i > rlt:
            rlt = i

    print(f'#{tc} {rlt}')
```



# 2. Baby gin 

```python
import sys

sys.stdin = open('input.txt')

T = int(input())

for tc in range(T):
    Num = map(int, input())
    count = [0]*12
    tri = 0
    run = 0

	# 입력값의 각 숫자 개수를 세어 count에 저장
    for i in Num:
        count[i] += 1

	# 9, 0, 1을 비교하기 위해 count 연장
    count[10], count[11] = count[0], count[1]

	# 2번 반복 (숫자에서 tri 혹은 run이 발생하는 것도 판별하기 위함)
    for _ in range(2):
		# index 9까지 탐색
        for i in range(len(count)-2):
			# 연이은 숫자가 1개 이상일 때
            if count[i] >= 1 and count[i+1] >= 1 and count[i+2] >= 1:
                count[i] -= 1
                count[i+1] -= 1
                count[i+2] -= 1
                run += 1
			# 한 숫자가 3개 이상일 때
            if count[i] >= 3:
                count[i] -= 3
                tri += 1

    if run + tri == 2:
        rlt = 1
    else:
        rlt = 0

    print(f'#{tc+1} {rlt}')
```



# 3. SWEA - 1206

https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV134DPqAA8CFAYh

```python
import sys

sys.stdin = open('input.txt')

for tc in range(1, 11):
    # 테스트 케이스의 길이
    N = int(input())
    # 건물 형태
    buildings = list(map(int, input().split()))
    # 세대 수를 세기 위한 변수
    cnt = 0

    # 개별 건물 인덱스, 양쪽 맨 끝 2칸에는 건물이 없음
    for i in range(2, len(buildings)-2):
        # 주변 건물 중 가장 높은 건물 높이 blind
        blind = 0
        for j in [buildings[i-2], buildings[i-1], buildings[i+1], buildings[i+2]]:
            if j > blind:
                blind = j

        # 건물이 주변 건물 최대 높이보다 크다면, 그 차이만큼 세대수에 더함
        if buildings[i] > blind:
            cnt += buildings[i] - blind

    print(f'#{tc} {cnt}')
```

