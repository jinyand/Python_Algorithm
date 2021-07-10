# [DP] 편집 거리

- 2021-07-10

```python
def edit_dist(str1, str2):
  n = len(str1)
  m = len(str2)

  # n * m 2차원 배열
  dp = [[0] * (m+1) for _ in range(n+1)]

  for i in range(1, n+1):
    dp[i][0] = i

  for j in range(1, m+1):
    dp[0][j] = j

  for i in range(1, n+1):
    for j in range(1, m+1):
      # 문자가 같은 경우
      if str1[i-1] == str2[j-1]:
        dp[i][j] = dp[i-1][j-1]
      # 문자가 다른 경우
      else:
        dp[i][j] = 1 + min(dp[i-1][j], dp[i-1][j-1], dp[i][j-1])

  return dp[n][m]

str1 = input()
str2 = input()

print(edit_dist(str1, str2))
```

- 두 문자가 다른 경우 : 왼쪽(삽입), 위쪽(삭제), 왼쪽 위(교체)에 해당하는 수 중에서 가장 작은 수에 1을 더해 대입
