# [DP] 멀리 뛰기

- 2021-09-24

```python
def solution(n):
    answer = 0
    
    if n < 2:
        return n
    
    dp = [0] * (n+1)
    
    dp[1] = 1
    dp[2] = 2
    
    for i in range(3, n+1):
        dp[i] = (dp[i-1] + dp[i-2]) % 1234567
        
    answer = dp[n]
    
    return answer
```

- n칸 뛰는 가짓수 = n-1 칸 뛴 후 1칸 뛰기 + n-2 칸 뛴 후 2칸 뛰기
