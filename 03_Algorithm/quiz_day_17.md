# 1. SWEA-5185

https://swexpertacademy.com/main/learn/course/subjectDetail.do?courseId=AVuPDYSqAAbw5UW6&subjectId=AWUYDLaK1kMDFAVT#

```python
# 이진수
T = int(input())
for tc in range(1, T+1):
    A = input().split()
    N = int(A[0])
    hex_num = A[1]
    dic = {
        '0': '0000',
        '1': '0001',
        '2': '0010',
        '3': '0011',
        '4': '0100',
        '5': '0101',
        '6': '0110',
        '7': '0111',
        '8': '1000',
        '9': '1001',
        'A': '1010',
        'B': '1011',
        'C': '1100',
        'D': '1101',
        'E': '1110',
        'F': '1111'
    }
    bin_num = ''

    for i in hex_num:
        bin_num += dic[i]

    print(f'#{tc} {bin_num}')
```



# 2. SWEA-5186

https://swexpertacademy.com/main/learn/course/subjectDetail.do?courseId=AVuPDYSqAAbw5UW6&subjectId=AWUYDLaK1kMDFAVT#

```python
# 이진수2
T = int(input())
for tc in range(1, T+1):
    N = float(input())

    i = -1
    bin_num = '0.'
    while True:
        # 나누어떨어지면 break
        if N == 0:
            print(f'#{tc} {bin_num[2:]}')
            break

        # bin_num 가 소수점 아래 12자리를 넘어가면 overflow
        elif len(bin_num) > 14:
            print(f'#{tc} overflow')
            break

        elif N // (2**i) > 0:
            bin_num += '1'
            N -= 2**i
            i -= 1

        else:
            bin_num += '0'
            i -= 1

```



# 3. SWEA-1242

https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV15JEKKAM8CFAYD

```python
# 암호코드 스캔
import sys
sys.stdin = open('sample.txt')

T = int(input())
for tc in range(1, T+1):
    # N 세로크기, M 가로크기
    N, M = map(int, input().split())
    # 중복제거
    arr = sorted(list(set([input() for _ in range(N)])))
    # 의미없는 행 제거
    arr.pop(0)
    dic = {
        '0': '0000',
        '1': '0001',
        '2': '0010',
        '3': '0011',
        '4': '0100',
        '5': '0101',
        '6': '0110',
        '7': '0111',
        '8': '1000',
        '9': '1001',
        'A': '1010',
        'B': '1011',
        'C': '1100',
        'D': '1101',
        'E': '1110',
        'F': '1111'
    }

    P = {
        (2, 1, 1): 0,
        (2, 2, 1): 1,
        (1, 2, 2): 2,
        (4, 1, 1): 3,
        (1, 3, 2): 4,
        (2, 3, 1): 5,
        (1, 1, 4): 6,
        (3, 1, 2): 7,
        (2, 1, 3): 8,
        (1, 1, 2): 9,
    }

    bin_arr = []
    # 배열 안의 16진수를 2진수로 변환
    for r in range(len(arr)):
        temp = ''
        for c in range(M):
            temp += dic[arr[r][c]]
        # 암호의 끝은 항상 1
        bin_arr.append(temp.rstrip('0'))

    visited = []
    rlt = 0
    for i in range(len(bin_arr)):
        bin = bin_arr[i]
        code = []
        n1 = n2 = n3 = 0
        # 뒤에서부터 탐색, 숫자 하나씩 끊기
        for j in range(len(bin)-1, -1, -1):
            if bin[j] == '1' and n2 == 0:               # 처음 1을 만나면
                n1 += 1                                 # 1의 개수를 세
            elif bin[j] == '0' and n3 == 0:             # 그 다음 0을 만나면
                n2 += 1                                 # 0의 개수를 세
            elif bin[j] == '1':                         # 다시 1을 만나면
                n3 += 1                                 # 1의 개수를 세
            elif bin[j] == '0' and bin[j-1] == '1':     # 다음 숫자 만나기 전까지 0 건너뛰고
                # 저장된 n1, n2, n3의 비율에 해당하는 숫자를 적어둬
                gcd = min(n1, n2, n3)
                code.append(P[(n3//gcd, n2//gcd, n1//gcd)])
                # 다음거 적으려면 초기화해
                n1 = n2 = n3 = 0

                # 8자가 적혔을 때
                if len(code) == 8:
                    # 정상 암호코드라면 (code[0]이 8번 숫자)
                    if not ((code[1]+code[3]+code[5]+code[7])*3 + code[0]+code[2]+code[4]+code[6]) % 10:
                        if code not in visited:
                            rlt += sum(code)
                            visited.append(code)
                    # 다시 하게 초기화해
                    code = []

    print(f'#{tc} {rlt}')

```

