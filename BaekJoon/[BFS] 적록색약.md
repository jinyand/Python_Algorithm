# [BFS] 적록색약

- 2021-09-09

```python
from collections import deque

n = int(input())
graph = [list(input()) for _ in range(n)]

dx = [-1, 0, 1, 0]
dy = [0, -1, 0, 1]

def bfs(x, y):
  q = deque()
  q.append((x, y))
  visited[x][y] = 1

  while q:
    x, y = q.popleft()
    
    for i in range(4):
      nx = x + dx[i]
      ny = y + dy[i]

      if 0 <= nx < n and 0 <= ny < n:
        if graph[x][y] == graph[nx][ny] and visited[nx][ny] == 0:
          visited[nx][ny] = 1
          q.append((nx, ny))

visited = [[0] * n for _ in range(n)]

answer = 0
rg_answer = 0

# 적록색약이 아닌 사람
for i in range(n):
  for j in range(n):
    if visited[i][j] == 0:
      answer += 1
      bfs(i, j)

# 적록색약 그래프로 변경
for i in range(n):
  for j in range(n):
    if graph[i][j] == 'G':
      graph[i][j] = 'R'

# 적록색약인 사람
visited = [[0] * n for _ in range(n)]
for i in range(n):
  for j in range(n):
    if visited[i][j] == 0:
      rg_answer += 1
      bfs(i, j)

print(answer, rg_answer)
```
