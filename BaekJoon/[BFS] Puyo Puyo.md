# [BFS] Puyo Puyo

- 2022-02-12

```python
from collections import deque

graph = [list(input().strip()) for _ in range(12)]
answer = 0

dx = [-1, 0, 1, 0]
dy = [0, -1, 0, 1]

def bfs(i, j, char):
  q = deque()
  q.append((i, j))
  pang.append((i, j))

  while q:
    x, y = q.popleft()
    for i in range(4):
      nx = x + dx[i]
      ny = y + dy[i]

      if 0 <= nx < 12 and 0 <= ny < 6:
        if visited[nx][ny] == 0 and graph[nx][ny] == char:
          visited[nx][ny] = 1
          q.append((nx, ny))
          pang.append((nx, ny))

def down():
  for i in range(6):
    for j in range(10, -1, -1):
      for k in range(11, j, -1): # 위아래 비교
        if graph[j][i] != '.' and graph[k][i] == '.':
          graph[k][i] = graph[j][i]
          graph[j][i] = '.'
          break

def delete(pang):
  # 동일 색 4개 이상 = pang 뿌요 부수기
  for x, y in pang:
    graph[x][y] = '.'

while True:
  flag = 0
  visited = [[0] * 6 for _ in range(12)]

  for i in range(12):
    for j in range(6):
      if graph[i][j] != '.' and visited[i][j] == 0:
        visited[i][j] = 1
        pang = []
        bfs(i, j, graph[i][j])

        if len(pang) >= 4:
          # 4개 이상의 뿌요가 뭉쳤을 때 flag = 1
          flag = 1
          # flag = 1일 경우 뿌요 삭제
          # 여러개의 뿌요 그룹이 쌓여도 1연쇄로 친다
          delete(pang)

  # flag = 0 이면 더 이상 사라질 뿌요 없다는 뜻 = break
  if flag == 0:
    break

  down()
  answer += 1

print(answer)
```
