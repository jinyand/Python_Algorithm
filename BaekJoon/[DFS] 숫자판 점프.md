# [DFS] 숫자판 점프

- 2022-03-06

```python
graph = [list(map(str, input().split())) for _ in range(5)]

dx = [0, -1, 0, 1]
dy = [-1, 0, 1, 0]

def dfs(x, y, num):
  if len(num) == 6:
    if num not in result:
      result.append(num)
    return

  for i in range(4):
    nx = x + dx[i]
    ny = y + dy[i]

    if 0 <= nx < 5 and 0 <= ny < 5:
      dfs(nx, ny, num + graph[nx][ny])

result = []
for i in range(5):
  for j in range(5):
    dfs(i, j, graph[i][j])

print(len(result))
```
