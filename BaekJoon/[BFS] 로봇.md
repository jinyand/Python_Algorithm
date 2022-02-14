# [BFS] 로봇

- 2022-02-14

```python
from collections import deque

m, n = map(int, input().split())
graph = [list(map(int, input().split())) for _ in range(m)]

sx, sy, sd = map(int, input().split())
ex, ey, ed = map(int, input().split())

# 동서남북
dx = [0, 0, 1, -1]
dy = [1, -1, 0, 0]
# 방향 바꾸기
# 동, 서 (0, 1) 라면 남, 북 (2, 3) 방향으로 전환
c_dir = [(2, 3), (2, 3), (0, 1), (0, 1)]

def bfs():
  q = deque()
  q.append((sx-1, sy-1, sd-1, 0))

  # 동서남북 정보를 모두 담을 수 있도록 3차원 배열 * 4
  visited = [[[0] * 4 for _ in range(n)] for _ in range(m)]
  visited[sx-1][sy-1][sd-1] = 1

  while q:
    x, y, d, cnt = q.popleft()
    
    if x == ex-1 and y == ey-1 and d == ed-1:
      return cnt

    # 1, 2, 3칸 직진
    for i in range(1, 4):
      nx = x + dx[d] * i
      ny = y + dy[d] * i
      nd = d

      if 0 <= nx < m and 0 <= ny < n:
        if graph[nx][ny] == 1:
          break
        if not visited[nx][ny][nd]:
          q.append((nx, ny, nd, cnt+1))
          visited[nx][ny][nd] = 1

    # 방향 바꾸기
    for nd in c_dir[d]:
      if not visited[x][y][nd]:
        q.append((x, y, nd, cnt+1))
        visited[x][y][nd] = 1

print(bfs())
```

- visited를 맵 크기대로 그리고, 각 방향(동서남북) 정보를 다 담아서 저장
- 1, 2, 3칸 전진하는 for문에서 벽(1) 만나면 break
- c_dir 설명 : [0, 1, 2, 3] = [(2, 3), (2, 3), (0, 1), (0, 1)] 마스킹해서 90도 회전한 두 가지 경우를 모두 저장
