https://swexpertacademy.com/main/learn/course/subjectDetail.do?courseId=AVuPDN86AAXw5UW6&subjectId=AWOVFCzaqeUDFAWg#

# 1. Min-Max

```python
T = int(input())

for tc in range(1, T+1):
    N = int(input())

    nums = list(map(int, input().split()))

    #max
    max_val = 0
    for i in nums:
        if max_val < i:
            max_val = i

    #min
    min_val = 1000000
    for i in nums:
        if min_val > i:
            min_val = i

    print(f'#{tc} {max_val-min_val}')
```



# 2. Electric Bus

```python
T = int(input())

for tc in range(1, T+1):
    # K = 충전 후 이동할 수 있는 구간
    # N = 종점 (0 ~ N)
    # M = 충전기 개수
    K, N, M = map(int, input().split())

    chargers = [0] +  list(map(int, input().split()))

    # 현재 버스 위치 i
    i = 0
    # 충전 횟수 cnt, -1부터 시작, 출발지부터 충전하는 개념으로 변경
    cnt = -1

    while True:
        # 현재 위치에서 충전 후 이동 가능한 정류장
        dis = list(range(i, i+K+1))

        # 현재 위치에서 종점까지 갈 수 있다면 break
        if N in dis:
            cnt += 1
            break

        # 현재 위치에서 갈 수 있는 가장 먼 정류장까지
        # 다음 충전소가 없다면 0 출력, break
        elif dis[-1] < chargers[chargers.index(i)+1]:
            cnt = 0
            break

        else:
            # 최대한 멀리갈 수 있는 정류장을 찾기위해 뒤에서부터 탐색
            for j in dis[::-1]:
                # 갈 수 있는 정류장 중 충전소가 있다면
                if j in chargers:
                    # 1회 충전 후, 버스는 충전소로 이동
                    cnt += 1
                    i = j
                    break

    print(f'#{tc} {cnt}')
```





# 3. Cards

```python
T = int(input())

for tc in range(1, T+1):
    N = int(input())
    nums = list(map(int, input()))

    # cnt_lst는 각 숫자의 개수를 담을 리스트
    cnt_lst = [0] * 10

    for i in nums:
        cnt_lst[i] += 1

    # cnt_list 를 순회하며 max_val 에는 등장한 횟수를
    # gn 에는 인덱스(가장 많이 등장한 숫자)를 저장
    max_val = 0
    gn = None
    for i in range(len(cnt_lst)):
        # 등장횟수가 같은 때는 숫자가 큰 쪽을 출력하므로
        # 등호 조건을 포함한다
        if max_val <= cnt_lst[i]:
            max_val = cnt_lst[i]
            gn = i

    print(f'#{tc} {gn} {max_val}')

```



# 4. Sum of Intervals

```python
T = int(input())

for tc in range(1, T+1):
    N, M = map(int, input().split())

    nums = list(map(int, input().split()))

    max_sum = 0
    # 각 정수는 최대 10000
    min_sum = 10000 * M

    # d_nums = [0, 1, ... , M]
    d_nums = list(range(M))

    for i in range(len(nums)-M+1):
        # 인덱스 i 에서부터 0, 1, ..., M을 더해가며 sum 누적
        sum = 0
        for j in d_nums:
            sum += nums[i+j]

        # 최댓값 최솟값 갱신
        if max_sum < sum:
            max_sum = sum
        if min_sum > sum:
            min_sum = sum

    print(f'#{tc} {max_sum-min_sum}')
```



# 5. SWEA - 1208 Flatten

```python
import sys

sys.stdin = open('input.txt')

def dump(boxes):
    highest = 0
    lowest = 100
    highest_idx = None
    lowest_idx = None

    # boxes 를 순회하며 최대, 최소값과 그 위치를 저장
    for i in range(len(boxes)):
        if highest < boxes[i]:
            highest = boxes[i]
            highest_idx = i
        if lowest > boxes[i]:
            lowest = boxes[i]
            lowest_idx = i

    # 가장 높은 박스더미에서 가장 낮은 박스더미로 하나 이동
    boxes[highest_idx] -= 1
    boxes[lowest_idx] += 1

    # 덤프 이후에 최대, 최소가 바뀌었는지 다시 점검
    new_highest = 0
    new_lowest = 100
    new_highest_idx = None
    new_lowest_idx = None

    for i in range(len(boxes)):
        if new_highest < boxes[i]:
            new_highest = boxes[i]
            new_highest_idx = i
        if new_lowest > boxes[i]:
            new_lowest = boxes[i]
            new_lowest_idx = i

    # 바뀐 후의 높이차를 구함
    dif = boxes[new_highest_idx] - boxes[new_lowest_idx]

    # 덤프된 리스트와 높이차를 반환
    return (boxes, dif)

# 테스트케이스 개수는 10
T = 10
for tc in range(1, T + 1):
    # 덤프 횟수
    repeat = int(input())
    boxes = list(map(int, input().split()))

    dif = 100
    # 주어진 덤프횟수만큼 반복
    for _ in range(repeat):
        # 평탄화가 완료되었을 경우, break
        if dif <= 1:
            print(f'#{tc} {dif}')
            break
        else:
            boxes, dif = dump(boxes)

    print(f'#{tc} {dif}')
```

