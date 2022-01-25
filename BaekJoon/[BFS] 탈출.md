# [BFS] 탈출

- 2022-01-25

```python
from collections import deque
import sys
input = sys.stdin.readline

r, c = map(int, input().split())
forest = [list(input().rstrip()) for _ in range(r)]
distance = [[0] * c for _ in range(r)]

dx = [-1, 0, 1, 0]
dy = [0, -1, 0, 1]

q = deque()

def bfs(Dx, Dy):
  
  while q:
    x, y = q.popleft()

    if forest[Dx][Dy] == 'S':
      return distance[Dx][Dy]

    for i in range(4):
      nx = x + dx[i]
      ny = y + dy[i]

      if 0 <= nx < r and 0 <= ny < c:

        # 돌이 있는 위치라면
        if forest[nx][ny] == 'X':
          continue

        # 현재 물 위치이며, 다음 이동할 칸이 비어있는 곳이거나 고슴도치일 경우
        if forest[x][y] == '*':
          if forest[nx][ny] == '.' or forest[nx][ny] == 'S':
            forest[nx][ny] = '*'
            q.append((nx, ny))

        # 현재 고슴도치 위치이며, 다음 이동할 칸이 비어있는 곳이거나 비버의 굴일 경우
        if forest[x][y] == 'S':
          if forest[nx][ny] == '.' or forest[nx][ny] == 'D':
            forest[nx][ny] = 'S'
            distance[nx][ny] = distance[x][y] + 1
            q.append((nx, ny))

  return "KAKTUS" # 위의 return 조건에 해당하지 않는 경우

# 고슴도치를 먼저 이동시켜도
# 그 위를 물이 덮어쓰게됨
for x in range(r):
  for y in range(c):
    if forest[x][y] == 'S': # 고슴도치 위치
      q.append((x, y))
    if forest[x][y] == 'D': # 비버의 굴
      d_x, d_y = x, y

for x in range(r):
  for y in range(c):
    if forest[x][y] == '*': # 물
      q.append((x, y))

# 비버의 집 위치로 bfs를 돌렸을 때
# 해당 칸이 'S' 고슴도치 이면 distance 값 반환
# 고슴도치가 아니라면 'KAKTUS' 반환
print(bfs(d_x, d_y))
```
