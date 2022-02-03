# [BFS] 벽 부수고 이동하기

- 2022-02-03

```python
from collections import deque

n, m = map(int, input().split())
graph = [list(map(int, input().strip())) for _ in range(n)]

dx = [-1, 0, 1, 0]
dy = [0, -1, 0, 1]

def bfs():
  q = deque()
  q.append((0, 0, 1))
  visited = [[[0] * 2 for _ in range(m)] for _ in range(n)]
  visited[0][0][1] = 1

  while q:
    a, b, c = q.popleft()
    # c = 0 : 벽을 한번 뚫은 상태
    # c = 1 : 아직 안뚫은 상태

    if a == n-1 and b == m-1:
      return visited[a][b][c]

    for i in range(4):
      nx = a + dx[i]
      ny = b + dy[i]

      if 0 <= nx < n and 0 <= ny < m:
        # 벽을 만났을 때, 현재 벽을 뚫을 수 있는 경우
        if graph[nx][ny] == 1 and c == 1:
          visited[nx][ny][0] = visited[a][b][c] + 1
          q.append((nx, ny, 0))
        
        # 벽이 아니고, 아직 방문하지 않은 곳인 경우
        if graph[nx][ny] == 0 and visited[nx][ny][c] == 0:
          visited[nx][ny][c] = visited[a][b][c] + 1
          q.append((nx, ny, c))

  return -1

print(bfs())
```

- 벽을 부순 상태와 아닌 상태를 3차원 배열로 구분
