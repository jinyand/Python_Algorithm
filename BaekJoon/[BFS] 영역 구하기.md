# [BFS] 영역 구하기

- 2021-10-06

```python
from collections import deque

m, n, k = map(int, input().split())

dx = [-1, 0, 1, 0]
dy = [0, -1, 0, 1]

graph = [[0] * n for i in range(m)]

for i in range(k):
  x1, y1, x2, y2 = map(int, input().split())
  for i in range(y1, y2):
    for j in range(x1, x2):
      graph[i][j] = -1

answer = []

for i in range(m):
  for j in range(n):
    # 빈 영역 만날 때
    if graph[i][j] == 0:
      count = 1
      q = deque([])
      q.append([i, j])
      graph[i][j] = 1

      while q:
        y, x = q.popleft()
        
        for k in range(4):
          nx = x + dx[k]
          ny = y + dy[k]

          if 0 <= nx < n and 0 <= ny < m and graph[ny][nx] == 0:
            graph[ny][nx] = 1
            q.append([ny, nx])
            count += 1

      answer.append(count)

print(len(answer))
answer.sort()
for i in answer:
  print(i, end=' ')
```
