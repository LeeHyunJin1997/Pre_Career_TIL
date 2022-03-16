# 1. SWEA-1231

https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV140YnqAIECFAYD

```python
# 중위순회

# 가장 첫 번째 출력할 노드 번호를 찾아주는 함수
def find_start(idx):
    if len(tree[idx]) == 1:
        return tree[idx][0]
    else:
        new_idx = tree[idx][1]
        return find_start(new_idx)


# 주어진 노드와 연결된 부모 노드를 찾는 함수
def find_parent(num):
    rlt = False
    for i in range(len(tree)):
        for j in range(1, len(tree[i])):
            if tree[i][j] == num:
                rlt = tree[i][0]
    return rlt


T = 10
for tc in range(1, T+1):
    # N 노드의 수
    N = int(input())
    tree = [list(input().split()) for _ in range(N)]
    # 인덱스와 노드 번호 일치
    words = ['None']

    for i in range(len(tree)):
        words.append(tree[i][1])
        tree[i].pop(1)
        tree[i] = list(map(int, tree[i]))
    # 인덱스와 노드 번호 일치
    tree = [[]] + tree

    visited = []

    # 가장 좌측 아래 노드 찾아 방문
    start = find_start(1)
    visited.append(start)
    print(f'#{tc} {words[start]}', end='')

    temp = start
    # visited 가 노드 개수만큼 생기면 중지
    while True:
        if len(visited) > N-1:
            print()
            break
        # 부모 노드로 올라가서 출력하고
        temp = find_parent(temp)
        if temp not in visited:
            visited.append(temp)
            print(f'{words[temp]}', end='')
        # 부모노드의 자식노드 중에 안 가본게 있으면
        for i in range(1, len(tree[temp])):
            if tree[temp][i] not in visited:
                # 가장 아랫단으로 이동해 출력
                temp = find_start(tree[temp][2])
                visited.append(temp)
                print(f'{words[temp]}', end='')
```

