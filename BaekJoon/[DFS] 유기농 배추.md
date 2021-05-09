# [DFS] 유기농 배추

- 2021-05-09
- 1012번

```python
def dfs(x, y):
  dx = [-1, 0, 1, 0]
  dy = [0, -1, 0, 1]

  for i in range(4):
    nx = x + dx[i]
    ny = y + dy[i]

    if 0 <= nx < n and 0 <= ny < m:
      if graph[nx][ny] == 1:
        graph[nx][ny] = -1
        dfs(nx, ny)
        
t = int(input())

for _ in range(t):
  m, n, k = map(int, input().split())
  graph = [[0] * m for _ in range(n)]
  count = 0

  for _ in range(k):
    a, b = map(int, input().split())
    graph[b][a] = 1

  for i in range(n):
    for j in range(m):
      if graph[i][j] > 0:
        dfs(i, j)
        count += 1

  print(count)
```

- 가로길이 m, 세로길이 n ⇒ n 행 m 열
- 배추 구역을 발견할 때마다 dfs 돌리고 구역 count + 1
- 구역에 들어가 배추를 -1 로 바꿔주어 이미 방문했다는 표시 남김
