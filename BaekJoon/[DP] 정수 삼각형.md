# [DP] 정수 삼각형

- 2021-07-09
- 1932번

```python
n = int(input())
dp = []

for _ in range(n):
  dp.append(list(map(int, input().split())))

for i in range(1, n):
  for j in range(i+1):
    # 맨 왼쪽에서 내려오는 경우
    if j == 0:
      up_left = 0
    else:
      up_left = dp[i-1][j-1]
    
		# 바로 위에서 내려오는 경우
    if j == i:
      up_right = 0
    else:
      up_right = dp[i-1][j]

    dp[i][j] = dp[i][j] + max(up_left, up_right)

print(max(dp[n-1]))
```
