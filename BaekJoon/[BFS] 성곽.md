# [BFS] 성곽

- 2022-02-18

```python
from collections import deque

n, m = map(int, input().split())
graph = [list(map(int, input().split())) for _ in range(m)]
visited = [[0] * n for _ in range(m)]

# 서, 북, 동, 남 = 1, 2, 4, 8
dx = [0, -1, 0, 1]
dy = [-1, 0, 1, 0]

def bfs(i, j):
  q = deque()
  q.append((i, j))
  visited[i][j] = 1
  cnt = 1 # 방의 넓이

  while q:
    x, y = q.popleft()

    for k in range(4):
      nx = x + dx[k]
      ny = y + dy[k]

      if 0 <= nx < m and 0 <= ny < n and visited[nx][ny] == 0:
        # ex ) 11 = 1011 의 경우 1, 2, 4, 8로 & 연산 했을 때 11 & 4 = 0000
        # 0 : 벽이 뚫려있다 => bfs 수행
        # 그 외 : continue
        if k == 0:
          if 1 & graph[x][y]: continue
        if k == 1:
          if 2 & graph[x][y]: continue
        if k == 2:
          if 4 & graph[x][y]: continue
        if k == 3:
          if 8 & graph[x][y]: continue

        visited[nx][ny] = 1
        q.append((nx, ny))
        cnt += 1

  return cnt

ans1, ans2, ans3 = 0, 0, 0

for i in range(m):
  for j in range(n):
    if visited[i][j] == 0: # 방 한칸 검사 시작
      ans1 += 1
      ans2 = max(ans2, bfs(i, j))

for i in range(m):
  for j in range(n):
    num = 1
    while num < 9:
      if num & graph[i][j]: # 벽일 경우
        visited = [[0] * n for _ in range(m)]
        graph[i][j] -= num # 벽 하나 없애기
        ans3 = max(ans3, bfs(i, j))
        graph[i][j] += num # 벽 다시 복구
      num *= 2 # 1, 2, 4, 8 에 대해서만 수행

print(ans1)
print(ans2)
print(ans3)
```
