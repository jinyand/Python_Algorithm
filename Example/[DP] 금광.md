# [DP] 금광

- 2021-07-07
- p.375

```python
t = int(input())

for _ in range(t):
  n, m = map(int, input().split())
  array = list(map(int, input().split()))

  # 2차원 배열
  dp = []
  index = 0
  for i in range(n):
    dp.append(array[index:index+m])
    index += m

  for j in range(1, m):
    for i in range(n):
      #  왼쪽 위에서 오는 경우
      if i == 0: # 시작이 맨 위일때
        left_up = 0
      else:
        left_up = dp[i-1][j-1]

      # 왼쪽 아래에서 오는 경우
      if i == n-1: # 시작이 맨 아래일때
        left_down = 0
      else:
        left_down = dp[i+1][j-1]

      # 왼쪽에서 오는 경우
      left = dp[i][j-1]

      dp[i][j] = dp[i][j] + max(left_up, left_down, left)
  
  result = 0

  for i in range(n):
    result = max(result, dp[i][m-1])

  print(result)
```

- 편의상 array 변수 대신 dp 테이블에 초기 데이터를 담아서 구현
- 왼쪽 위, 왼쪽, 왼쪽 아래에서 오는 경우를 고려하기 때문에 dp 세로 탐색 범위를 1부터 m까지로 설정
- i == 0 : 맨 위의 행이 시작점 → 왼쪽 위에서 오는 경우 없음
- i == n-1 : 맨 아래의 행이 시작점 → 왼쪽 아래에서 오는 경우 없음
