# [DP] 등굣길

- 2021-08-29

```python
def solution(m, n, puddles):
    answer = 0
    
    dp = [[0] * (m+1) for _ in range(n+1)]
    dp[1][1] = 1
    
    puddles = [[i, j] for [j, i] in puddles]
    
    for i in range(1, n+1):
        for j in range(1, m+1):
            if i == 1 and j == 1:
                continue
            elif [i, j] in puddles:
                dp[i][j] = 0
            else:
                dp[i][j] = (dp[i-1][j] + dp[i][j-1]) % 1000000007
    
    answer = dp[n][m]
    
    return answer
```

- 좌표가 반대로 되어있다는 점을 고려해서 미리 puddles 좌표를 거꾸로 만듦
- 점화식 : 바로 위 칸까지의 경로 수 + 바로 왼쪽 칸까지의 경로수
