# [BFS] 케빈 베이컨의 6단계 법칙

- 2022-01-20

```python
from collections import deque

n, m = map(int, input().split())
graph = [[] for _ in range(n+1)]
result = []

def bfs(graph, start):
  num = [0] * (n+1)
  visited = [start]
  q = deque()
  q.append(start)

  while q:
    a = q.popleft()
    for i in graph[a]:
      if i not in visited:
        num[i] = num[a] + 1
        visited.append(i)
        q.append(i)

  return sum(num)

for i in range(m):
  a, b = map(int, input().split())
  graph[a].append(b)
  graph[b].append(a)

for i in range(1, n+1):
  result.append(bfs(graph, i))

print(result.index(min(result))+1)
```

- start에서 다른 노드로 갈 수 있을 때 num[다음 노드] = num[현재 노드] + 1 과 같이 1씩 더해주며 연결된 노드를 모두 순회한 후 num의 합을 리턴
