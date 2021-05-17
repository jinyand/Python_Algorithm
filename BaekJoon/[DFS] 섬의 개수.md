# [DFS] 섬의 개수

- 2021-05-17
- 4963번

```python
import sys
sys.setrecursionlimit(10000)
input = sys.stdin.readline

while True:
  w, h = map(int, input().split())
  graph = [list(map(int, input().split())) for _ in range(h)]

  visited = [[False] * w for _ in range(h)]

  if w == 0 and h == 0:
    break

  dx = [1, 1, 1, 0, -1, -1, -1, 0]
  dy = [-1, 0, 1, 1, 1, 0, -1, -1]

  def dfs(x, y):
    visited[x][y] = True
    for i in range(8):
      nx = x + dx[i]
      ny = y + dy[i]

      if 0 <= nx < h and 0 <= ny < w:
        if graph[nx][ny] == 1 and not visited[nx][ny]:
          dfs(nx, ny)

  count = 0

  for i in range(h):
    for j in range(w):
      if graph[i][j] == 1 and not visited[i][j]:
        dfs(i, j)
        count += 1

  print(count)
```

- 입출력 속도 : sys.stdin.readline() > raw_input() > input()
- 런타임 에러 방지 : 재귀함수가 있는 경우, 최대 재귀 깊이 설정
    - sys.setrecursionlimit(10000) : 10000까지 재귀 허용 깊이를 늘림
