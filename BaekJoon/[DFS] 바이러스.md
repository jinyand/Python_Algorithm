# [DFS] 바이러스

- 2021-05-07
- 2606번

```python
n = int(input()) # 컴퓨터의 수
m = int(input()) # 컴퓨터 쌍의 수

graph = [[] for _ in range(n+1)]
graph[0] = [0, 0]

for i in range(m):
  a, b = map(int, input().split())
  graph[a].append(b)
  graph[b].append(a)

virus = [False] * (n+1)

def dfs(graph, v, virus):
  virus[v] = True
  
  for i in graph[v]:
    if not virus[i]:
      dfs(graph, i, virus)

dfs(graph, 1, virus)

count = 0

for i in range(2, n+1):
  if virus[i] == True:
    count += 1

print(count)
```
