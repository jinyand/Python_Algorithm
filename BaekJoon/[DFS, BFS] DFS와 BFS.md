# [DFS, BFS] DFS와 BFS

- 2021-05-06
- 1260번

```python
from collections import deque

n, m, v = map(int, input().split())

graph = [[] for _ in range(n+1)]
graph[0] = [0, 0]
for i in range(m):
  a, b = map(int, input().split())
  graph[a].append(b)
  graph[b].append(a)
  graph[a].sort()
  graph[b].sort()

def dfs(graph, v, visited):
  visited[v] = True
  print(v, end=' ')
  for i in graph[v]:
    if not visited[i]:
      dfs(graph, i, visited)

def bfs(graph, v, visited):
  queue = deque([v])
  visited[v] = True

  while queue:
    v = queue.popleft()
    print(v, end=' ')

    for i in graph[v]:
      if not visited[i]:
        queue.append(i)
        visited[i] = True

  
visited = [False] * (n+1)
dfs(graph, v, visited)

visited = [False] * (n+1)
print()
bfs(graph, v, visited)
```

- 개념 복습할 겸 기본 문제. 각 리스트들의 범위 설정하는 부분에서 실수 줄이기
- 입력으로 주어지는 간선이 '양방향' 이라는 부분에서, graph 원소 추가할 때 a, b 에 대해 양방향으로 삽입하고 꼭 sort() 해주어야 한다.
