# [구현] n진수 게임

- 2021-08-25

```python
def solution(n, t, m, p):
    answer = ''
    array = []
    
    for i in range(t*m):
        cvt = convert(i, n)
        for c in cvt:
            array.append(c)
    
    for i in range(p-1, t*m, m):
        answer += array[i]
    
    return answer

# 10 -> n진법 변환 함수 (재귀함수 이용)
def convert(n, base):
    T = "0123456789ABCDEF"
    q, r = divmod(n, base)
    if q == 0:
        return T[r]
    else:
        return convert(q, base) + T[r]
```
