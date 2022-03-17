https://swexpertacademy.com/main/learn/course/subjectDetail.do?courseId=AVuPDN86AAXw5UW6&subjectId=AWOVJ-_6qfsDFAWg

# 1. SWEA-5178

```python
# 노드의 합
def make_tree():
    """
    BFS로 온전한 tree 구조(간선)을 생성
    :return: None
    """
    cnt = 1
    queue = [1]

    while True:
        if cnt > N - 1:
            break

        for _ in range(len(queue)):
            temp = queue.pop(0)

            cnt += 1
            tree[temp][0] = cnt
            queue.append(cnt)
            if cnt > N - 1:
                break

            cnt += 1
            tree[temp][1] = cnt
            queue.append(cnt)
            if cnt > N - 1:
                break


def cal(node):
    """
    해당 노드의 값을 계산하는 함수
    :param node: 현재 노드
    :return: 현재 노드의 값이 있을 때는 그대로 반환, 없을 때는 하위 노드의 합을 계산
    """
    if tree[node][2]:
        return tree[node][2]
    # 오른쪽 자식이 없는 경우
    elif not tree[node][1]:
        return cal(tree[node][0])
    else:
        return cal(tree[node][0]) + cal(tree[node][1])


T = int(input())
for tc in range(1, 1+T):
    # N 노드 개수, M 리프노드 개수, L 출력할 노드 번호
    N, M, L = map(int, input().split())
    leaves = [list(map(int, input().split())) for _ in range(M)]

    # 왼쪽 자식 노드, 오른쪽 자식 노드, 값 저장
    tree = [[0 for _ in range(3)] for _ in range(N + 1)]
    make_tree()

    # 리프노드에 값 저장
    for i in leaves:
        tree[i[0]][2] = i[1]

    print(f'#{tc} {cal(L)}')
```



# 2. SWEA-5174

```python
# subtree
def count(node):
    """
    하위 노드 개수를 세는 함수
    :param node: 현재 노드
    :return: None
    """
    global cnt
    if node:
        cnt += 1
        count(tree[node][0])
        count(tree[node][1])


T = int(input())
for tc in range(1, T+1):
    # E 간선 개수, N 노드 개수
    E, N = map(int, input().split())
    edges = list(map(int, input().split()))

    tree = [[0, 0, 0] for _ in range(E+2)]

    for i in range(0, len(edges)-1, 2):
        parent_node = edges[i]  # 현재노드, 부모노드
        child_node = edges[i + 1]  # 자식노드

        if tree[parent_node][0] == 0:
            tree[parent_node][0] = child_node

        else:
            tree[parent_node][1] = child_node

        tree[child_node][2] = parent_node

    cnt = 0

    count(N)

    print(f'#{tc} {cnt}')

```



# 3. SWEA-5176

```python
# 이진탐색
def make_tree():
    """
    BFS로 tree 의 간선을 생성
    :return: None
    """
    cnt = 1
    Q = [1]

    while True:
        if cnt > N-1:
            break

        for _ in range(len(Q)):
            temp = Q.pop(0)

            cnt += 1
            tree[temp][0] = cnt
            Q.append(cnt)
            if cnt > N-1:
                break

            cnt += 1
            tree[temp][1] = cnt
            Q.append(cnt)
            if cnt > N-1:
                break


def inorder(node):
    """
    중위순회하며 값을 저장하는 함수
    :param node: 노드 번호
    :return: None
    """
    global num
    if node:
        inorder(tree[node][0])
        tree[node][2] = num
        num += 1
        inorder(tree[node][1])


T = int(input())
for tc in range(1, T+1):
    # N 노드 개수
    N = int(input())

    # 왼쪽 자식 노드, 오른쪽 자식 노드, 값 저장
    tree = [[0 for _ in range(3)] for _ in range(N+1)]

    make_tree()

    num = 1
    inorder(1)

    # 루트(1번 노드)에 저장된 값과 N//2 번 노드에 저장된 값 출력
    print(f'#{tc} {tree[1][2]} {tree[N//2][2]}')
```



# 4. SWEA-5177

```python
# 이진 힙
def make_tree():
    """
    BFS로 tree의 간선을 생성
    :return: None
    """
    cnt = 1
    queue = [1]

    while True:
        if cnt > N:
            break

        for _ in range(len(queue)):
            temp = queue.pop(0)

            if cnt > N:
                break

            # 좌우 자식에게 반복
            for i in range(2):
                cnt += 1
                if cnt > N:
                    break

                tree[temp][i] = cnt
                queue.append(cnt)
                tree[cnt][2] = temp


def compare(node):
    """
    부모노드와 값을 비교하는 함수
    :param node: 현재노드
    :return: None
    """
    parent = tree[node][2]
    # 부모노드가 존재할 때만 진행
    if parent:
        # 부모노드의 값이 더 크다면
        if tree[node][3] < tree[parent][3]:
            # 값을 바꿔
            tree[node][3], tree[parent][3] = tree[parent][3], tree[node][3]
    else:
        return

    # 부모노드도 반복
    compare(parent)


def an_sum(node):
    """
    해당 노드의 조상 노드의 합을 구하는 함수
    :param node: 현재 노드
    :return: 함수 재호출
    """
    global rlt
    if node == 1:
        return 0

    parent = tree[node][2]
    # 결과값에 조상 노드 값들을 쌓아감
    rlt += tree[parent][3]
    return an_sum(parent)


T = int(input())
for tc in range(1, 1+T):
    N = int(input())
    values = list(map(int, input().split()))
    # 왼쪽 자식 노드, 오른쪽 자식노드, 부모노드, 값
    tree = [[0 for _ in range(4)] for _ in range(N + 1)]

    make_tree()

    # values의 각 값을 tree에 배정
    for i in range(N):
        tree[i+1][3] = values[i]

    # 비교를 반복해 정렬
    for i in range(1, N+1):
        compare(i)

    rlt = 0

    # 마지막 노드 = N번째 노드
    last_node = N
    an_sum(last_node)

    print(f'#{tc} {rlt}')
```



# 5. SWEA-1232

https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV141J8KAIcCFAYD

```python
# 사칙연산
import sys
sys.stdin = open('input.txt')


def cal(node):
    """
    하위 노드들의 계산을 수행하는 함수
    :param node: 현재 노드
    :return: 각 단계에서 계산 결과
    """
    left_child = tree[node][0]
    right_child = tree[node][1]

    # 현재 노드가 리프노드 일때
    if tree[node][2].isdigit():
        return int(tree[node][2])

    elif tree[node][2] == '*':
        return cal(left_child) * cal(right_child)
    elif tree[node][2] == '/':
        return cal(left_child) / cal(right_child)
    elif tree[node][2] == '+':
        return cal(left_child) + cal(right_child)
    elif tree[node][2] == '-':
        return cal(left_child) - cal(right_child)


T = 10
for tc in range(1, T+1):
    # N 노드 수
    N = int(input())
    edges = [list(input().split()) for _ in range(N)]

    # [왼쪽 자식노드, 오른쪽 자식노드, 값]
    tree = [[0 for _ in range(3)] for _ in range(N + 1)]

    # edges로 받아온 입력을 tree에 맞는 형태로 옮김
    for i in range(len(edges)):
        if len(edges[i]) == 4:
            tree[int(edges[i][0])][0] = int(edges[i][2])
            tree[int(edges[i][0])][1] = int(edges[i][3])
            tree[int(edges[i][0])][2] = edges[i][1]
        elif len(edges[i]) == 2:
            tree[int(edges[i][0])][2] = edges[i][1]

    print(f'#{tc} {int(cal(1))}')

```

