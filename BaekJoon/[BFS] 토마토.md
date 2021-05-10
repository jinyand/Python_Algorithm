# [BFS] 토마토

- 2021-05-10
- 7576번

```python
from collections import deque

m, n = map(int, input().split())
box = [list(map(int, input().split())) for _ in range(n)]

dx = [-1, 0, 1, 0]
dy = [0, -1, 0, 1]

queue = deque()

for i in range(n):
  for j in range(m):
    if box[i][j] == 1:
      queue.append([i, j])

while queue:
  x, y = queue.popleft()
      
  for i in range(4):
    nx = x + dx[i]
    ny = y + dy[i]

    if 0 <= nx < n and 0 <= ny < m:
      if box[nx][ny] == 0:
        box[nx][ny] = box[x][y] + 1
        queue.append([nx, ny])
          
flag = False
result = -1

for b in box:
  for i in b:
    if i == 0:
      flag = True
      break
    result = max(result, i)

if flag: # 모두 익지않은 상태
  print(-1)
elif result == 1: # 모두 익어있는 상태
  print(0)
else:
  print(result-1)
```

- 토마토를 익히는 작업을 반복할 때 마다 익힌 토마토에 1을 더해주어 마지막으로 익힌 토마토의 값 = 토마토가 모두 익을 때까지의 최소 날짜 가 되게 한다.
