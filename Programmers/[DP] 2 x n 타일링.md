# [DP] 2 x n 타일링

- 2021-09-28

```python
def solution(n):
    answer = 0
    
    dp = [0 for i in range(n+1)]
    
    dp[1] = 1
    dp[2] = 2
    
    for i in range(3, n+1):
        dp[i] = (dp[i-1] + dp[i-2]) % 1000000007
    
    answer = dp[n]
    
    return answer
```

- 점화식은 dp[i] = dp[i-1] + dp[i-2] 쉽게 알수있음
