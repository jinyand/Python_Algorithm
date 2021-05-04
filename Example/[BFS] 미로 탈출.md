# [BFS] 미로 탈출

- 2021-05-04
- p.152

```python
from collections import deque

n, m = map(int, input().split())

graph = []
for i in range(n):
  graph.append(list(map(int, input())))

# 이동할 네 방향 정의 (상하좌우)
dx = [-1, 1, 0, 0]
dy = [0, 0, -1, 1]
  
def bfs(x, y):
  queue = deque()
  queue.append((x, y))

  while queue:
    x, y = queue.popleft()
    for i in range(4):
      nx = x + dx[i]
      ny = y + dy[i]
      
      if nx < 0 or ny < 0 or nx >= n or ny >= m:
        continue

      if graph[nx][ny] == 0:
        continue

      if graph[nx][ny] == 1:
        graph[nx][ny] = graph[x][y] + 1
        queue.append((nx, ny))

  return graph[n-1][m-1]
    

print(bfs(0, 0))
```

- 특정한 노드를 방문하면 그 이전 노드의 거리에 1을 더한 값을 리스트에 넣고, 맨 오른쪽 하단의 값을 출력
