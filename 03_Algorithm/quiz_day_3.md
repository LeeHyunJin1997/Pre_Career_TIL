# 연습문제 1.

- 5x5 행렬에서 (각 원소 - 상하좌우 원소)의 절댓값의 합을 구하라.

```python
num_list = []

for i in range(5):
    row = [j+5*i for j in range(1, 6)] # 한 줄로 반복된 원소를 가진 리스트를 생성하는 방식
    num_list.append(row)

# 변화량 값을 갖는 델타. 각각 상, 하, 좌, 우를 의미
dr = [-1, 1, 0, 0]
dc = [0, 0, -1, 1]
total = 0

# 행 선택
for r in range(len(num_list)):
    # 열 선택
    for c in range(len(num_list[0])):
        for k in range(4):
            each_row = r + dr[k]
            each_col = c + dc[k]

            # Index Error를 방지하기 위한 조건
            if each_row < 0 or each_row > 4 or each_col < 0 or each_col > 4:
                continue
            else:
                sub = num_list[r][c] - num_list[each_row][each_col]

                # 삼항연산자
                sub = sub if sub >= 0 else -sub
                total += sub

print(total)

```

