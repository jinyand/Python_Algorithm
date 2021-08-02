# [bfs] 안전 영역

- 2021-08-02
- 2468번

```python
from collections import deque

n = int(input())
graph = [list(map(int, input().split())) for _ in range(n)]

max = max(map(max, graph))

dx = [-1, 0, 1, 0]
dy = [0, -1, 0, 1]

def bfs(x, y, h, visited):
  q = deque()
  q.append((x, y))
  visited[x][y] = 1

  while q:
    x, y = q.popleft()
    
    for i in range(4):
      nx = x + dx[i]
      ny = y + dy[i]

      if 0 <= nx < n and 0 <= ny < n:
        if graph[nx][ny] > h and visited[nx][ny] == 0:
          visited[nx][ny] = 1
          q.append((nx, ny))

max_area = 0

for h in range(max):
  # 높이가 달라질 때마다 초기화 되어야하는 변수들
  answer = 0
  visited = [[0] * n for _ in range(n)]

  for i in range(n):
    for j in range(n):
      if graph[i][j] > h and visited[i][j] == 0:
        bfs(i, j, h, visited)
        answer += 1

  if max_area < answer:
    max_area = answer

print(max_area)
```

- max(map(max, graph))) 로 그래프에서 가장 큰 수를 구하여 0부터 max-1까지의 높이 별로 영역 수를 계산 (max를 높이로 적용하면 모두 물에 잠기기 때문)
