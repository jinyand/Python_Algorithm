# [DFS] 트리의 부모 찾기

- 2021-10-07

```python
import sys
input = sys.stdin.readline
sys.setrecursionlimit(10**9)

n = int(input())

graph = [[] for i in range(n+1)] # 트리
parent = [0 for i in range(n+1)] # 부모노드

for i in range(n-1):
  a, b = map(int, input().split())
  graph[a].append(b)
  graph[b].append(a)

def dfs(start, graph, parent):
  # 연결된 노드 탐색
  for i in graph[start]:
    if parent[i] == 0:
      parent[i] = start
      dfs(i, graph, parent)

dfs(1, graph, parent)

for i in range(2, n+1):
  print(parent[i])
```

- 주의해야할 점 : 재귀함수의 최대 깊이를 늘려줘야 런타임 에러가 발생하지 않음 `sys.setrecursionlimit(10**9)`
