# [DP] 1로 만들기

- 2022-03-25

```python
import sys
input = sys.stdin.readline

n = int(input())
dp = [0] * (n+1)

for i in range(2, n+1):
  # 1을 빼는 경우로 먼저 저장
  dp[i] = dp[i-1] + 1
  # 3 or 2로 나누어질 때
  if i % 3 == 0:
    dp[i] = min(dp[i], dp[i//3]+1)
  if i % 2 == 0:
    dp[i] = min(dp[i], dp[i//2]+1)

print(dp[n])
```
