# [구현] k진수에서 소수 개수 구하기

- 2022-02-27

```python
import string
import math

def solution(n, k):
    answer = 0
    convert_n = convert(n, k)
    
    p_list = convert_n.split('0')
    p_list = [v for v in p_list if v]
    
    for num in p_list:
        if is_prime_number(int(num)):
            answer += 1
    
    return answer

tmp = string.digits + string.ascii_lowercase

def convert(num, base) :
    q, r = divmod(num, base)
    if q == 0 :
        return tmp[r] 
    else :
        return convert(q, base) + tmp[r]
    
# 소수 판별 함수
def is_prime_number(n):
    if n == 0 or n == 1:
        return False
    else:
        for i in range(2, int(math.sqrt(n) + 1)):
            if n % i == 0:
                # 1 이외의 수로 나눠지면 False
                return False
            
        return True
```

- 코테에서 풀었던 문제 백업
