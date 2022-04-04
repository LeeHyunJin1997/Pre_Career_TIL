# 트리

- 원소 간 계층 관계를 가짐
- 원소 간 1: n 관계를 가짐
- 상위 원소에서 하위 원소로 확장



# 트리 용어

- 노드 : 트리의 원소

- 간선 : 노드를 연결하는 선

- 서브 트리 : 트리 속의 트리, 하부 트리 구조

- 루트 노드 : 최상위 노드

- 형제 노드 : 같은 부모를 갖는 자식 노드

- 조상 노드 : 해당 노드에서 루트 노드까지 올라가는 경로에 있는 노드

- 자손 노드 : 해당 노드를 루트 노드로 하는 서브 트리의 노드

- 노드의 차수 : 해당 노드에 연결되어 있는 노드 수

- 트리의 차수 : 트리에 있는 노드의 차수 중 가장 큰 값

- 리프 노드 (단말 노드) : 자식 노드가 없는 노드

- 노드의 높이 (레벨) : 루트에서 해당 노드에 이르는 간선의 수

- 트리의 높이 : 노드의 높이 중 가장 큰 값

  

# 이진 트리

- 모든 노드가 최대 2개의 자식 노드를 갖는 트리



### 포화 이진 트리 (Full Binary Tree)

- 리프 노드를 제외한 모든 노드가 2개의 자식 노드를 갖는 이진트리
- 루트 노드를 1번으로 하여 `2^h+1 - 1` 개의 노드를 가짐
  - h = 높이



### 완전 이진 트리 (Complete Binary Tree)

- 노드의 개수가 n 개일 때, n번 노드까지 빈 자리가 없는 이진 트리



### 편향 이진 트리 (Skewed Binary Tree)

- 각 노드들의 한쪽 방향의 자식 노드만을 가진 이진 트리

- 높이 h 에 대한 최소 노드 개수를 가짐

  

# 순회

- 트리의 각 노드를 중복되지 않게 전부 방문하는 것
- 전위순회 (preorder traversal, VLR)
  - Vertex - Left -Right : 부모, 왼쪽 자식, 오른쪽 자식 순으로 방문

```python
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
```



- 중위순회 (inorder traversal, LVR)
  - Left - Vertex - Right : 왼쪽 자식, 부모, 오른쪽 자식 순으로 방문

```python
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
```



- 후위순회 (posterorder traversal, LRV)
  - Left - Right - Vertex : 왼쪽 자식, 오른쪽 자식, 부모 순으로 방문

```python
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
```



# 이진 트리의 표현

- 노드 번호의 규칙성을 이용해 트리를 배열로 표현 가능

  - 노드 i 의 부모노드 : i // 2

  - 노드 i 의 왼쪽 자식 노드 : i * 2

  - 노드 i의 오른쪽 자식 노드 : i * 2 + 1



- 단점
  - 편향 이진 트리를 배열로 나타낼 경우, 사용하지 않는 원소에 대해 메모리 공간 낭비 발생
  - 중간에 새로운 노드를 삽입하거나 노드를 삭제할 경우, 배열의 크기 변경 어려워 비효율적