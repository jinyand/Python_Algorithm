# [BFS] 불!

- 2022-03-02

```python
import sys
from collections import deque
input = sys.stdin.readline

r, c = map(int, input().split())
graph = [list(input().strip()) for _ in range(r)]

fq = deque()
jq = deque()

f_visited = [[0] * c for _ in range(r)]
j_visited = [[0] * c for _ in range(r)]

dx = [-1, 0, 1, 0]
dy = [0, -1, 0, 1]

def bfs():
  # 불의 움직임
  while fq:
    x, y = fq.popleft()

    for i in range(4):
      nx = x + dx[i]
      ny = y + dy[i]

      if 0 <= nx < r and 0 <= ny < c:
        if not f_visited[nx][ny] and graph[nx][ny] != '#':
          f_visited[nx][ny] = f_visited[x][y] + 1
          fq.append((nx, ny))

  # 지훈이의 움직임
  while jq:
    x, y = jq.popleft()

    for i in range(4):
      nx = x + dx[i]
      ny = y + dy[i]

      if 0 <= nx < r and 0 <= ny < c:
        if not j_visited[nx][ny] and graph[nx][ny] != '#':
          # 불이 퍼진 시간보다 지훈이가 이동한 시간이 더 빨라야한다
          # 아직 불이 도달하지 않았거나
          # 불보다 지훈이의 값이 더 작을 경우 (지훈이가 더 빨리 이동)
          if not f_visited[nx][ny] or f_visited[nx][ny] > j_visited[x][y] + 1:
            j_visited[nx][ny] = j_visited[x][y] + 1
            jq.append((nx, ny))

      else:
        # 범위 밖(미로 밖)으로 탈출했을 경우
        return j_visited[x][y] + 1

  return 'IMPOSSIBLE'
  
for i in range(r):
  for j in range(c):
    if graph[i][j] == 'F':
      fq.append((i, j))
    if graph[i][j] == 'J':
      jq.append((i, j))
      
print(bfs())
```
