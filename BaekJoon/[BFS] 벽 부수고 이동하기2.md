# [BFS] 벽 부수고 이동하기2

- 2022-03-09

```python
import sys
input = sys.stdin.readline
from collections import deque

n, m, k = map(int, input().split())
graph = [list(map(int, input().strip())) for _ in range(n)]

dx = [0, -1, 0, 1]
dy = [-1, 0, 1, 0]

def bfs(a, b, v):
  q = deque()
  q.append((a, b, v))

  visited = [[[0] * (k+1) for _ in range(m)] for _ in range(n)]
  # [0][0][k] : 벽을 한번도 부수지 않은 경우
  # k-1, k-2 .. 벽을 부술 수록 -1
  visited[0][0][k] = 1

  while q:
    x, y, c = q.popleft()

    if x == n-1 and y == m-1:
      return visited[x][y][c]

    for i in range(4):
      nx = x + dx[i]
      ny = y + dy[i]

      if 0 <= nx < n and 0 <= ny < m:
        if graph[nx][ny] == 0 and not visited[nx][ny][c]:
          visited[nx][ny][c] = visited[x][y][c] + 1
          q.append((nx, ny, c))

        # 벽이 있고, 부술 수 있을 경우
        if graph[nx][ny] == 1 and c > 0 and not visited[nx][ny][c-1]:
          visited[nx][ny][c-1] = visited[x][y][c] + 1
          q.append((nx, ny, c-1))

  return -1

print(bfs(0, 0, k))
```

- 조건문에서 c < k 를 했을 경우 시간 초과가 나서, visited[0][0][k]를 시작으로 하여 벽을 부술 때마다 c-1 배열에 넣어주어 조건문을 c > 0 로 선언했다.
