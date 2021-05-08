# [BFS] 경쟁적 전염

- 2021-05-08
- p.344

```python
from collections import deque

n, k = map(int, input().split())
graph = [list(map(int, input().split())) for _ in range(n)]
t_s, t_x, t_y = map(int, input().split())
virus = []

dx = [-1, 0, 1, 0]
dy = [0, -1, 0, 1]

for i in range(n):
  for j in range(n):
    if graph[i][j] != 0:
      virus.append((graph[i][j], 0, i, j)) # 번호, 시간, 좌표

virus.sort()

q = deque(virus)

while q:
  virus, s, x, y = q.popleft()

  # 주어진 시간이 될 때까지
  if s == t_s:
    break
  
  for i in range(4):
    nx = x + dx[i]
    ny = y + dy[i]

    if 0 <= nx < n and 0 <= ny < n:
      if graph[nx][ny] == 0:
        graph[nx][ny] = virus
        q.append((graph[nx][ny], s+1, nx, ny))

print(graph[t_x - 1][t_y - 1])
```

- 각 바이러스가 낮은 번호부터 증식한다는 점에서 queue를 사용해서 너비 우선 탐색 수행
- 먼저 주어진 그래프에서 바이러스만을 찾아내 (바이러스 번호, 시간, x좌표, y좌표)를 담은 리스트를 만들고 이를 정렬한 뒤 큐에 옮겨담는다.
- 큐를 돌면서 주어진 시간이 될 때까지 바이러스를 낮은 번호부터 증식시키는 것을 반복
- 증식된 바이러스는 큐에 추가로 삽입해준다.
