# [DFS] 음료수 얼려 먹기

- 2021-05-04
- p.149

```python
n, m = map(int, input().split())

graph = []
for i in range(n):
  graph.append(list(map(int, input())))

# dfs로 특정한 노드를 방문한 뒤에 연결된 모든 노드들도 방문
def dfs(x, y):
  if x <= -1 or x >= n or y <= -1 or y >= m:
    return False
  # 현재 노드를 아직 방문하지 않았다면
  if graph[x][y] == 0:
    graph[x][y] = 1
    # 상하좌우의 위치도 모두 재귀적으로 호출
    dfs(x, y-1)
    dfs(x, y+1)
    dfs(x+1, y)
    dfs(x-1, y)
    return True
  return False

result = 0
for i in range(n):
  for j in range(m):
    if dfs(i, j) == True:
      result += 1

print(result)
```

1. 특정한 지점의 주변 상하좌우를 살펴본 뒤에 주변 지점 중에서 값이 '0'이면서 아직 방문하지 않은 지점이 있다면 해당 지점을 방문한다.
2. 방문한 지점에서 다시 상하좌우를 살펴보면서 방문을 다시 진행하면, 연결된 모든 지점을 방문할 수 있다.
3. 1~2의 과정을 모든 노드에 반복하며 방문하지 않은 지점의 수를 센다.
- 1의 과정에서 주변 0 들이 다 1 로 채워지므로 결국 카운트 되는 값은 0 으로 이루어진 구역의 개수가 된다.
