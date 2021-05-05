# [DFS] 연구소

- 2021-05-05
- p.341

```python
n, m = map(int, input().split())
data = [] # 초기 맵
temp = [[0] * m for _ in range(n)] # 벽 설치 후 맵

for _ in range(n):
  data.append(list(map(int, input().split())))

dx = [-1, 0, 1, 0]
dy = [0, 1, 0, -1]

result = 0

# DFS로 각 바이러스가 사방으로 퍼지도록
def virus(x, y):
  for i in range(4):
    nx = x + dx[i]
    ny = y + dy[i]
    if nx >= 0 and nx < n and ny >= 0 and ny < m:
      if temp[nx][ny] == 0:
        temp[nx][ny] = 2
        virus(nx, ny)

# 현재 맵에서 안전 영역의 크기 계산
def get_score():
  score = 0
  for i in range(n):
    for j in range(m):
      if temp[i][j] == 0:
        score += 1
  return score

# DFS로 울타리 설치, 매번 안전 영역 크기 계산
def dfs(count):
  global result

  # 울타리가 3개 설치된 경우
  if count == 3:
    for i in range(n):
      for j in range(m):
        temp[i][j] = data[i][j]

    for i in range(n):
      for j in range(m):
        if temp[i][j] == 2:
          virus(i, j)

    result = max(result, get_score())
    return

  # 빈 공간에 울타리 설치
  for i in range(n):
    for j in range(m):
      if data[i][j] == 0:
        data[i][j] = 1
        count += 1
        dfs(count)
        # 벽을 세운 후에 다시 원상복귀 시켜주기
        data[i][j] = 0
        count -= 1

dfs(0)
print(result)
```

- 벽을 3개 설치하는 모든 경우의 수를 다 계산해야 한다. 벽의 개수가 3개가 되는 모든 조합을 찾은 뒤에 그러한 조합에 대해서 안전 영역의 크기를 계산하는 방식.
- 매번 벽을 설치할 때마다 바이러스를 사방으로 퍼지게 하여 안전 영역 계산 = 완전 탐색
