# 연습문제 1. 후위표기법

- 수식문자열을 읽어서 피연산자 출력
- 연산자는 스택에 push하여 수식이 끝나면 한번에 출력

```python
cal = ['+', '-', '*', '/']
T = int(input())
for tc in range(1, T+1):
    S = input()
    stack = []
    print(f'#{tc}', end=' ')

    for i in S:
        # 연산자라면
        if i in cal:
            # 스택 쌓기
            stack.append(i)
        # 아니라면
        else:
            # 그대로 출력
            print(i, end='')

    # 스택에 담겨있는 연산자 차례로 출력
    for _ in range(len(stack)):
        print(stack.pop(), end='')
    print()
```



# 연습문제 2. 부분집합

- [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]의 부분집합 중 합이 10인 것을 구하시오.

```python
def mySum(lst):
    total = 0
    for i in lst:
        total += i
    return total

def subset(idx, N, k):
    # 비트가 1인 원소만 모은 temp
    temp = [a[m] for m in range(len(a)) if (bit[m])]
    # 합이 목표와 같으면
    if mySum(temp) == k:
        print(temp)
        return
    # 인덱스가 끝까지 오면
    elif idx == N:
        return
    # 부분집합 생성
    else:
        bit[idx] = 0
        subset(idx+1, N, k)
        bit[idx] = 1
        subset(idx+1, N, k)

# a 는 1 ~ 10 의 리스트
a = [i for i in range(1,11)]
N = len(a)
bit = [0] * N
# 합이 10 인 부분집합 구하기
target = 10
subset(0, N, target)

```



# SWEA-1223

```python
for tc in range(1, 11):
    T = int(input())
    # 후위 표기식으로 변경
    S = input()
    cal_stack = []
    tail = ''
    for i in range(len(S)):
        # * 만나면 스택 쌓기
        if S[i] == '*':
            cal_stack.append(S[i])
        # + 만나면 저장되어 있던 스택 붙이기
        # + 를 스택에 쌓기
        elif S[i] == '+':
            while cal_stack:
                tail += cal_stack.pop()
            cal_stack.append(S[i])
        # 연산자가 아니면 이어붙이기
        else:
            tail += S[i]

    # 남아있는 스택 이어붙이기
    for _ in range(len(cal_stack)):
        tail += cal_stack.pop()

    rlt = []
    for i in tail:
        if i == '*':
            rlt.append(rlt.pop()*rlt.pop())
        elif i == '+':
            rlt.append(rlt.pop()+rlt.pop())
        else:
            rlt.append(int(i))

    print(f'#{tc} {rlt[0]}')
```

