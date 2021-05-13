# [BFS] 나이트의 이동

- 2021-05-13
- 7562번

```python
from collections import deque
  
dx = [-1, -2, -2, -1, 1, 2, 2, 1]
dy = [2, 1, -1, -2, -2, -1, 1, 2]

def bfs(nx, ny, mx, my):
  q = deque()
  q.append([nx, ny])
  data[nx][ny] = 1

  while q:
    x, y = q.popleft()
    
    if x == mx and y == my:
      print(data[mx][my]-1)
      return

    for i in range(8):
      ax = x + dx[i]
      ay = y + dy[i]
      if 0 <= ax < l and 0 <= ay < l and data[ax][ay] == 0:
        data[ax][ay] = data[x][y] + 1
        q.append([ax, ay])

t = int(input())

for _ in range(t):
  l = int(input()) # 한변의 길이
  nx, ny = map(int, input().split())
  mx, my = map(int, input().split())
  data = [[0] * l for _ in range(l)]
  bfs(nx, ny, mx, my)
```
