# 1. SWEA_4836

https://swexpertacademy.com/main/learn/course/subjectDetail.do?courseId=AVuPDN86AAXw5UW6&subjectId=AWOVF-WqqecDFAWg#

```python
T = int(input())

for tc in range(1, 1+T):
    N = int(input())

    nums = []
    red = set()
    blue = set()

    # 칠할 영역
    for _ in range(N):
        nums.append(list(map(int, input().split())))

    for i in nums:
        # 색상이 빨강이라면
        if i[-1] == 1:
            # 두 점 사이에 있는 좌표를 set 에 저장
            for j in range(i[0], i[2]+1):
                for k in range(i[1], i[3]+1):
                    red.add((j, k))

        # 파랑일 때
        else:
            for j in range(i[0], i[2]+1):
                for k in range(i[1], i[3]+1):
                    blue.add((j, k))

    # 빨강과 파랑의 교집합의 수를 출력
    print(f'#{tc} ', end='')
    print(len(red & blue))
```



# 2. SWEA_4837

https://swexpertacademy.com/main/learn/course/subjectDetail.do?courseId=AVuPDN86AAXw5UW6&subjectId=AWOVF-WqqecDFAWg#

```python
def mySum(lst):
    total = 0
    for i in lst:
        total += i
    return total

# A는 1~12
A = [i for i in range(1, 13)]

T = int(input())
for tc in range(1, T+1):

    # N = 원소의 수, K = 부분집합의 합
    N, K = map(int, input().split())

    n = len(A)
    cnt = 0

    for i in range(1 << n):
        sets = []

        # 부분집합 생성
        for j in range(n):
            if i & (1 << j):
                sets.append(A[j])

        # 길이가 N이고 값의 합이 K일때
        if len(sets) == N and mySum(sets) == K:
            cnt += 1

    print(f'#{tc} {cnt}')
```



# 3. SWEA_4839

https://swexpertacademy.com/main/learn/course/subjectDetail.do?courseId=AVuPDN86AAXw5UW6&subjectId=AWOVF-WqqecDFAWg#

```python
# 절반 부분을 구하는 함수
def half(start, end):
    return int((start+end)/2)


# 정답을 찾는 횟수를 구하는 함수
def find(start, end, target_page, cnt=0):
    # 절반부분이 목표 페이지일 때
    if half(start, end) == target_page:
        # 한번 더 세고 반환
        cnt += 1
        return cnt
    # 절반 부분이 찾는 부분보다 크다면
    elif half(start, end) > target_page:
        cnt += 1
        # 절반 부분을 end 에 두고 다시 찾아
        return find(start, half(start,end), target_page, cnt)
    else:
        cnt += 1
        return find(half(start, end), end, target_page, cnt)


T = int(input())
for tc in range(1, T+1):
    # P = 전체쪽수, Pa = A가 찾을 쪽, Pb = B가 찾을 쪽
    P, Pa, Pb = map(int, input().split())

    # A와 B가 목표 페이지를 찾는 데 걸린 횟수
    A = find(1, P, Pa)
    B = find(1, P, Pb)

    # 더 짧은 사람이 이김
    print(f'#{tc} ', end='')
    if A < B:
        print('A')
    elif A == B:
        print(0)
    else:
        print('B')
```



# 4. SWEA_4843

https://swexpertacademy.com/main/learn/course/subjectDetail.do?courseId=AVuPDN86AAXw5UW6&subjectId=AWOVF-WqqecDFAWg#

```python
T = int(input())
for tc in range(1, T+1):
    N = int(input())
    nums = list(map(int, input().split()))

    # 버블 정렬
    for j in range(len(nums)):
        for i in range(len(nums)-1):
            if nums[i] > nums[i+1]:
                nums[i], nums[i+1] = nums[i+1], nums[i]

    print(f'#{tc}', end=' ')
    # 뒤에서(최댓값) 하나씩, 앞에서(최솟값) 하나씩
    for i in range(5):
        print(nums[-i - 1], end=' ')
        print(nums[i], end=' ')

    print('')
```



# 5. SWEA_1210

https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV14ABYKADACFAYh

```python
# 전체 리스트와 뒤에서부터 x번 째 단계, 위치 인덱스 y를 인자로 받는 함수
def check(ladders, x, y):
    # 위치가 양쪽 끝 사다리라면, 확인 가능한 쪽만 진행
    if y == 99:
        # 옆으로 건너갈 다리를 만나면
        if ladders[x][y-1] == 1:
            while True:
                # 0 이면 멈춰
                if y == 0:
                    break
                # 쭉 가
                elif ladders[x][y-1] == 1:
                    y = y - 1
                else:
                    break
    elif y == 0:
        if ladders[x][y+1] == 1:
            while True:
                if y == 99:
                    break
                elif ladders[x][y+1] == 1:
                    y = y + 1
                else:
                    break
    else:
        if ladders[x][y+1] == 1:
            while True:
                if y == 99:
                    break
                elif ladders[x][y+1] == 1:
                    y = y + 1
                else:
                    break
        elif ladders[x][y-1] == 1:
            while True:
                if y == 0:
                    break
                elif ladders[x][y-1] == 1:
                    y = y - 1
                else:
                    break

    return y

for i in range(10):
    # 테스트 케이스 번호 N
    N = int(input())
    ladders = []

    for i in range(100):
        ladders.append(list(map(int, input().split())))

    # 도착점 번호 특정
    finish = ladders[-1].index(2)

    # check 후 이동 100번 반복
    y = finish
    for i in range(100):
        y = check(ladders, -(i+1), y)

    print(f'#{N} {y}')
```

