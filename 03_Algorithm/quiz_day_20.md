# 1. 연습문제1

```python
# 연습문제1: 퀵정렬
def quickSort(lst, begin, end):
    # begin이 end보다 작을 때(정렬할 것이 남아있을 때)
    if begin < end:
        p = partition(lst, begin, end)
        # p를 기준으로 좌측에서 반복
        quickSort(lst, begin, p-1)
        # p를 기준으로 우측에서 반복
        quickSort(lst, p+1, end)


# partition이 한번 호출되면
# a는 피봇을 기준으로
# 좌측에는 더 작은 값이, 우측에는 더 큰 값이
# 정렬되지 않은 상태로 섞여있음
def partition(lst, begin, end):
    # 기준이 되는 pivot (인덱스)
    pivot = (begin + end) // 2
    L = begin
    R = end
    # L과 R이 만나지 않을 때까지 반복
    while L < R :
        # L은 pivot 위치의 값보다 큰 값을 찾으며 우측으로 이동
        while L < R and lst[L]< lst[pivot]:
            L += 1
        # R은 pivot 위치의 값보다 작은 값을 찾으며 좌측으로 이동
        while L < R and lst[R] >= lst[pivot]:
            R -= 1
        # L과 R이 서로 만나지 않고 정지했을 때
        if L < R:
            # L이 피봇까지 왔으면 (pivot 좌측에는 큰 값이 더이상 없다면)
            if L == pivot:
                # 피봇을 R 위치로 변경
                pivot = R
            # R, L 값 바꿔
            lst[L], lst[R] = lst[R], lst[L]
    # while 문 종료 시점, L과 R 값은 동일
    # 피봇과 R 값 바꿔
    lst[pivot], lst[R] = lst[R], lst[pivot]
    return R


T = int(input())
for _ in range(T):
    a = list(map(int, input().split()))
    quickSort(a, 0, len(a)-1)
    print(' '.join(map(str, a)))

```



# 2. 연습문제 2

```python
# 연습문제 2: 부분집합
def powerset(idx, s):
    """
    부분집합을 출력
    :param idx: 현위치
    :param s: 현재까지 선택한 원소의 합
    :return: 종료조건일 때 종료
    """
    # 가지치기
    # 이미 원소의 합이 10을 넘었을 경우 그만
    if s > 10:
        return

    # 마지막 원소까지 선택을 마쳤을 때
    if idx == len(p):
        if s == 10:
            for i in range(len(bit)):
                if bit[i]:
                    print(p[i], end=' ')
            print()
        return

    else:
        # 해당 원소를 선택한 경우
        bit[idx] = 1
        powerset(idx+1, s+p[idx])
        # 해당 원소를 선택하지 않은 경우
        bit[idx] = 0
        powerset(idx+1, s)


p = [x for x in range(1, 11)]
bit = [0] * len(p)

powerset(0, 0)

```



# 3. 연습문제 3

```python
# 연습문제 3: 전위순회, 중위순회, 후위순회
def preorder(node):
    """
    전위순회
    :param node: 노드 번호
    :return: None
    """
    if node:
        # root 방문
        print(node, end=' ')
        # 왼쪽방문
        preorder(tree[node][0])
        # 오른쪽방문
        preorder(tree[node][1])


def inorder(node):
    """
    중위순회
    :param node: 노드 번호
    :return: None
    """
    if node:
        # 왼쪽 방문
        inorder(tree[node][0])
        # root 방문
        print(node, end=' ')
        # 오른쪽 방문
        inorder(tree[node][1])


# 후위순회 (postorder)
def postorder(node):
    """
    후위순회
    :param node: 노드 번호
    :return: None
    """
    if node:
        # 왼쪽 방문
        postorder(tree[node][0])
        # 오른쪽 방문
        postorder(tree[node][1])
        # root 방문65
        print(node, end=' ')


# V 정점 개수
V = int(input())
edges = list(map(int, input().split()))
# 트리 구조: 왼쪽 자식 - 오른쪽 자식 - 부모노드
tree = [[0 for _ in range(3)] for _ in range(V+1)]

# 입력받은 간선을 부모-자식 단위로 자르기
for i in range(0, len(edges)-1, 2):
    parent_node = edges[i] # 부모노드
    child_node = edges[i+1] # 자식노드

    # 트리에 자식노드가 하나도 그려져 있지 않을때
    if tree[parent_node][0] == 0:
        tree[parent_node][0] = child_node
    # 이미 왼쪽 자식노드가 그려져 있을 때
    else:
        tree[parent_node][1] = child_node

    # 자식노드에게도 누가 부모인지 알려주기
    tree[child_node][2] = parent_node

start_node = 1
print('전위순회 : ', end='')
preorder(start_node)
print()
print('중위순회 : ', end='')
inorder(start_node)
print()
print('후위순회 : ', end='')
postorder(start_node)
print()

```



# 4. SWEA-5204

```python
# 병합정렬
def merge_sort(lst):
    global cnt
    # 원소가 하나 남으면 반환
    if len(lst) < 2:
        return lst

    mid = len(lst) // 2
    low_lst = merge_sort(lst[:mid])
    high_lst = merge_sort(lst[mid:])

    # low_arr 와 high_arr 를 앞에서부터 비교, 더 작은 것을 merged_lst 로 복사
    merged_lst = []
    l = h = 0
    while l < len(low_lst) and h < len(high_lst):
        if low_lst[l] <= high_lst[h]:
            merged_lst.append(low_lst[l])
            l += 1
        else:
            merged_lst.append(high_lst[h])
            h += 1

    # 오른쪽이 먼저 복사된 경우 카운트
    if low_lst[l:]:
        cnt += 1

    # low_arr 와 high_arr 중 하나만 전부 이동시켰을 때
    # 남은 원소 이어붙이기
    merged_lst += low_lst[l:]
    merged_lst += high_lst[h:]
    return merged_lst


T = int(input())
for tc in range(1, T+1):
    # 정수의 개수
    N = int(input())
    lst = list(map(int, input().split()))

    cnt = 0
    lst = merge_sort(lst)
    print(f'#{tc} {lst[N//2]} {cnt}')

```

