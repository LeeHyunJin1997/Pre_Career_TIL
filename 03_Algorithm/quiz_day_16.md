# 1. SWEA-1240

https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV15FZuqAL4CFAYD

```python
# 단순 2진 암호코드
import sys
sys.stdin = open('input.txt')

# 0 ~ 9까지의 수와 대응하는 이진 코드
P = {
    '0001101': 0,
    '0011001': 1,
    '0010011': 2,
    '0111101': 3,
    '0100011': 4,
    '0110001': 5,
    '0101111': 6,
    '0111011': 7,
    '0110111': 8,
    '0001011': 9,
}

T = int(input())
for tc in range(1, T+1):
    # N 세로 크기, M 가로크기
    N, M = map(int, input().split())
    arr = [input() for _ in range(N)]

    # 암호가 입력된 줄 찾기
    code = None
    for r in range(N):
        for c in range(M):
            # 같은 암호코드가 반복되니 그 줄만 만나면 그만둬
            if arr[r][c] == '1':
                code = arr[r]
                break
        if code:
            break

    # 그 줄에서도 암호 부분만 추출
    # 뒤에서부터 탐색
    for i in range(len(code)-1, -1, -1):
        # 1을 만나면 암호코드 길이인 56 자리 저장
        if code[i] == '1':
            code = code[i-55:i+1]
            break

    # 다시 코드를 7자리씩 끊어 숫자로 변환
    decode = []
    for i in range(0, len(code), 7):
        decode.append(P[code[i:i+7]])

    # 변환된 숫자의 검증코드 확인
    # 홀수자리합*3 + 짝수자리합 + 검증코드가 10으로 나눠떨어져야 정상암호
    verify = (decode[0]+decode[2]+decode[4]+decode[6])*3 + decode[1]+decode[3]+decode[5] + decode[7]
    # 정상암호일 때
    if verify % 10 == 0:
        print(f'#{tc} {sum(decode)}')
    else:
        print(f'#{tc} 0')
```

