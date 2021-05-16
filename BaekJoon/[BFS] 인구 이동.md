# [BFS] 인구 이동

- 2021-05-16
- 16234번

```python
from collections import deque

n, l, r = map(int, input().split())
graph = [list(map(int, input().split())) for _ in range(n)]

dx = [-1, 0, 1, 0]
dy = [0, -1, 0, 1]

def check(x, y, index):
  united = []
  united.append((x, y))

  q = deque()
  q.append((x, y))

  union[x][y] = index # 현재 연합 번호
  summary = graph[x][y] # 현재 연합 인구 수
  count = 1 # 현재 연합 국가 수

  while q:
    x, y = q.popleft()
    for i in range(4):
      nx = x + dx[i]
      ny = y + dy[i]

      if 0 <= nx < n and 0 <= ny < n and union[nx][ny] == -1:
        # 1번 과정
        if l <= abs(graph[nx][ny] - graph[x][y]) <= r:
          q.append((nx, ny))
          union[nx][ny] = index # 연합에 추가
          summary += graph[nx][ny]
          count += 1
          united.append((nx, ny))

  for i, j in united:
    graph[i][j] = summary // count # 연합 국가들끼리 인구 이동

  return count

result = 0

while True:
  union = [[-1] * n for _ in range(n)]
  index = 0
  for i in range(n):
    for j in range(n):
      if union[i][j] == -1:
        check(i, j, index)
        index += 1

  if index == n*n:
    break
  
  result += 1

print(result)
```

- united : (x, y)의 위치와 연결된 나라(연합) 정보를 담는 리스트
- union : 현재 연합의 처리 여부 / -1인 경우 : 아직 처리되지 않음
