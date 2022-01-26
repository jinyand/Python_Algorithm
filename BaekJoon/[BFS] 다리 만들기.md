# [BFS] 다리 만들기

- 2022-01-26

```python
import sys
from collections import deque
input = sys.stdin.readline

n = int(input())
graph = [list(map(int, input().split())) for _ in range(n)]
visited = [[False] * n for _ in range(n)]
count = 1 # 섬의 개수
answer = sys.maxsize

dx = [-1, 0, 1, 0]
dy = [0, -1, 0, 1]

# 섬의 개수 count 하는 bfs
def bfs_count(a, b):
  q = deque()
  q.append((a, b))
  visited[a][b] = True
  graph[a][b] = count
  
  while q:
    x, y = q.popleft()

    for i in range(4):
      nx = x + dx[i]
      ny = y + dy[i]

      if 0 <= nx < n and 0 <= ny < n:
        if not visited[nx][ny] and graph[nx][ny] == 1:
          visited[nx][ny] = True
          graph[nx][ny] = count
          q.append((nx, ny))
    
# 섬을 잇는 최단 거리 구하는 bfs
def bfs_distance(a):
  global answer
  dist = [[-1] * n for _ in range(n)] # 거리 저장
  q = deque()

  # 섬들의 위치 모두 큐에 저장
  # 섬 = 0, 바다 = -1
  for i in range(n):
    for j in range(n):
      if graph[i][j] == a:
        q.append((i, j))
        dist[i][j] = 0

  while q:
    x, y = q.popleft()

    for i in range(4):
      nx = x + dx[i]
      ny = y + dy[i]

      if 0 <= nx < n and 0 <= ny < n:
        # 다른 섬을 만났을 경우 최단 거리 저장 후 리턴
        if graph[nx][ny] > 0 and graph[nx][ny] != a:
          answer = min(answer, dist[x][y])
          return

        # 바다를 만났을 경우 거리 + 1
        if graph[nx][ny] == 0 and dist[nx][ny] == -1:
          dist[nx][ny] = dist[x][y] + 1
          q.append((nx, ny))

# 섬의 개수 구하기
for a in range(n):
  for b in range(n):
    if not visited[a][b] and graph[a][b] == 1:
      bfs_count(a, b)
      count += 1

# 최단 거리 구하기
for a in range(1, count):
  bfs_distance(a)

print(answer)
```

- bfs를 두개 사용해야한다
    1. 섬의 개수 카운트
    2. 섬을 잇는 최단거리 계산
- 1에서 섬을 그룹핑하여 2에서 바로 다른 섬을 인지할 수 있도록 함
