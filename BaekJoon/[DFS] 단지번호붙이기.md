# [DFS] 단지번호붙이기

- 2021-05-07
- 2667번

```python
n = int(input()) # 지도의 크기 n x n
map = [list(map(int, input())) for _ in range(n)]

count = 0

dx = [-1, 0, 1, 0]
dy = [0, -1, 0, 1]

visited = [[False] * n for _ in range(n)]

def dfs(x, y):
  global count
  count += 1
  visited[x][y] = True

  for i in range(4):
    nx = x + dx[i]
    ny = y + dy[i]

    if 0 <= nx < n and 0 <= ny < n:
      if map[nx][ny] == 1 and visited[nx][ny] == False:
        dfs(nx, ny)
    

result = 0
sector = []

for i in range(n):
  for j in range(n):
    if map[i][j] == 1 and visited[i][j] == False:
      count = 0
      dfs(i, j)
      result += 1
      sector.append(count)

print(result)
sector.sort()

for i in range(len(sector)):
  print(sector[i])
```

- 단지를 나누고 각 단지 안의 집 수도 출력해야 하므로, 지도에서 '방문하지 않은 단지의 집'을 발견했을 때 단지의 수를 1 더해준 다음 dfs 함수 안에서 각 집을 재귀적으로 방문.
- 집을 방문하는 과정에서 count를 1 더해주며 방문하고 각 단지의 집 수, 즉 count 값을 dfs 함수가 끝난 뒤 list로 만들어서 보관한다.
