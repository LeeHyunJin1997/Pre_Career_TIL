# 1.

- 스택에 1, 2, 3을 담은 후 pop해 하나씩 출력해보라.

```python
stack = []
stack.append(1)
stack.append(2)
stack.append(3)
print(stack.pop())	# 3
print(stack.pop())	# 2
print(stack.pop())	# 1
```



# 2.

- 소괄호의 짝을 검사하는 프로그램을 만들어라.

```python
# 괄호 짝 검사
def check(n):
    stack = []
    for i in n:
        # 괄호 만나면
        if i == '(':
            # 스택 쌓기
            stack.append(i)
        # 괄호 닫으면
        elif i == ')':
            # 꺼낼 수 있으면 꺼내고
            if len(stack):
                stack.pop()
            # 못 꺼내면 틀린거야
            else:
                return False
    if len(stack) == 0:
        return True
    # 다 꺼냈는데 남는게 있어? 틀렸네
    else:
        return False

n = input()
print(check(n))
```



# 3.

![image-20220222112313839](quiz_day_8.assets/image-20220222112313839.png)

![image-20220222112333979](quiz_day_8.assets/image-20220222112333979.png)

```python
# pascal 함수는 선언된 리스트에 다음 줄을 이어붙임
def pascal():
    global lst
    # 마지막 줄보다 길이를 1 늘린 리스트 (양쪽 끝에 1)
    temp = [1] + [0] * (len(lst[-1])-1) + [1]
    # 새로 생긴 줄의 각 항목은 전 줄의 i-1과 i의 합
    for i in range(1, len(temp)-1):
        temp[i] = lst[-1][i-1] + lst[-1][i]
    # 글로벌 lst 에 추가해
    lst.append(temp)

T = int(input())
for tc in range(1, T+1):
    N = int(input())

    # 첫 줄은 항상 1
    lst = [[1]]

    # pascal 함수를 N-1번 반복
    for _ in range(N-1):
        pascal()

    # lst 안의 각 항목을 줄별로 출력
    print(f'#{tc}')
    for i in lst:
        for j in i:
            print(j, end=' ')
        print('')
```