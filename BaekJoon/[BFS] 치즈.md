# [BFS] 치즈

- 2022-03-13

```python
from collections import deque

dx = [-1, 0, 1, 0]
dy = [0, -1, 0, 1]

def bfs():
  q = deque()
  q.append((0, 0))

  visited = [[0] * m for _ in range(n)]
  visited[0][0] = 1
  
  c_cnt = 0 # 녹은 치즈 수
  
  while q:
    x, y = q.popleft()

    for i in range(4):
      nx = x + dx[i]
      ny = y + dy[i]

      if 0 <= nx < n and 0 <= ny < m and not visited[nx][ny]:
        # 치즈가 아닌 곳을 만났을 때 => 계속 탐색
        if graph[nx][ny] == 0:
          q.append((nx, ny))
          visited[nx][ny] = 1

        # 치즈를 만났을 때
        # 치즈는 q에 넣어서 탐색 x => 가장자리를 확인해야하기 때문
        if graph[nx][ny] == 1:
          graph[nx][ny] = 0 # 녹여준다
          c_cnt += 1
          visited[nx][ny] = 1

  # 한시간(while)이 지날 때마다 녹은 치즈 수를 배열에 추가
  cheese.append(c_cnt)
  return c_cnt

n, m = map(int, input().split())
graph = [list(map(int, input().split())) for _ in range(n)]
cheese = []

time = 0
while True:
  time += 1
  cnt = bfs()
  if cnt == 0: # 녹은 치즈수가 없을 때
    break

print(time-1)
print(cheese[-2])
```
