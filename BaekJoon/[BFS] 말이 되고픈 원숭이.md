# [BFS] 말이 되고픈 원숭이

- 2022-01-21

```python
from collections import deque

k = int(input())
w, h = map(int, input().split())
graph = [list(map(int, input().split())) for _ in range(h)]

# 동서남북
dx = [-1, 0, 1, 0]
dy = [0, -1, 0, 1]

# 말 = 체스의 나이트
# 두칸 전진 후 좌 or 우 한칸 전진
hx = [-2, -1, 1, 2, -2, -1, 1, 2]
hy = [1, 2, 2, 1, -1, -2, -2, -1]

# k개의 특수이동 고려 => 3차원 검사 배열
check = [[[False] * (k+1) for _ in range(w)] for _ in range(h)]

# (a, b)에서 시작
def bfs(a, b):
  q = deque()
  q.append((a, b, 0, 0))
  check[a][b][0] = True

  while q:
    # x좌표, y좌표, 특수이동 횟수(말 이동), 동작 횟수
    x, y, horse, cnt = q.popleft()

    # 현재 좌표가 도착점이라면
    if x == h-1 and y == w-1:
      return cnt
    
    # 동서남북
    for i in range(4):
      nx = x + dx[i]
      ny = y + dy[i]
      
      if 0 <= nx < h and 0 <= ny < w:
        if check[nx][ny][horse] == False:
          if graph[nx][ny] == 0:
            check[nx][ny][horse] = True
            q.append((nx, ny, horse, cnt+1))

    # k 스킬 사용 횟수가 남아있는 경우
    # 특수이동
    if horse < k:
      for i in range(8):
        nx = x + hx[i]
        ny = y + hy[i]

        if 0 <= nx < h and 0 <= ny < w:
          # 현재 특수이동으로 가려는 정점은
          # cnt + 1 번째에 방문하게 되는 것이므로
          # check[nx][ny][horse+1]을 체크해야한다
          if check[nx][ny][horse+1] == False:
            if graph[nx][ny] == 0:
              check[nx][ny][horse+1] = True
              q.append((nx, ny, horse+1, cnt+1))

  return -1

print(bfs(0, 0))
```

- 말 이동(특수이동)으로 이동하는 경우를 고려하여 check라는 3차원 검사 배열을 따로 만들어 현재 특수 이동 횟수에 따라 해당 정점을 방문했는지 안했는지 중복 검사
- 가장 먼저 도착점에 도착하는 경우가 최소 경우이므로 cnt 출력
