# DP 알고리즘 (Dynamic Planning)



# DFS (깊이우선탐색)

- 한 반향으로 갈 수 있는 경로로 깊이 탐색하다가 더 이상 진행할 수 없을 때 갈림길으로 돌아옴
- 스택을 이용하여 구현
  - 시작 정점 v를 결정
  - 방문하지 않은 w가 있다면, v를 push한 후에 w 방문
  - 방문하지 않은 정점이 없다면 pop하여 되돌아가 탐색 방향을 바꿈

```python
visited = []
stack = []
DFS(v)
	v 방문;
    visited[v] <- true;
    do {
        if (v의 인접 정점 중 방문 안한 w 찾기)
        	push(v);
        	while( w ){
                w 방문;
                visited[w] <- true;
                push(w);
                v<-w;
                v의 인접 정점 중 방문 안한 w 찾기
            }
        	v<-pop(stack);
    } while(v)
end DFS()
```



# BFS (너비우선탐색)

- 큐를 이용하여 구현



# 계산기

- 문자열로 된 계산식이 주어질 때, 스택을 이용하여 계산 가능
  - 중위표기법
    - A+B
  - 후위표기법
    - AB+

- 구현

1. 중위표기법에서 후위표기법으로 변환
2. 

