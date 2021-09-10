# [BFS] 토마토(3차원)

- 2021-09-10

```python
from collections import deque
import sys

input = sys.stdin.readline
m, n, h = map(int, input().split())
box = [[list(map(int, input().split())) for _ in range(n)] for _ in range(h)]
visited = [[[0] * m for _ in range(n)] for _ in range(h)]

dx = [-1, 1, 0, 0, 0, 0]
dy = [0, 0, -1, 1, 0, 0]
dz = [0, 0, 0, 0, -1, 1]

q = deque()

def bfs():
  while q:
    z, x, y = q.popleft()

    for i in range(6):
      nx = x + dx[i]
      ny = y + dy[i]
      nz = z + dz[i]

      if 0 <= nx < n and 0 <= ny < m and 0 <= nz < h:
        if box[nz][nx][ny] == 0 and visited[nz][nx][ny] == 0:
          visited[nz][nx][ny] = 1
          box[nz][nx][ny] = box[z][x][y] + 1
          q.append((nz, nx, ny))

for i in range(h):
  for j in range(n):
    for k in range(m):
      if box[i][j][k] == 1:
        q.append((i, j, k))
        visited[i][j][k] = 1
        
bfs()

flag = 0
result = 0

for i in box:
  for j in i:
    for k in j:
      if k == 0:
        print(-1)
        exit(0)
      result = max(result, k)

print(result-1)
```

- 3차원 배열 [z][x][y] 순서를 헷갈리지 않는게 중요
