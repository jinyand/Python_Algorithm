# [BFS] 효율적인 해킹

- 2022-03-10

```python
import sys
input = sys.stdin.readline
from collections import deque

n, m = map(int, input().split())
graph = [[] for _ in range(n+1)]

for _ in range(m):
  a, b = map(int, input().split())
  graph[b].append(a)

def bfs(start):
  q = deque()
  q.append(start)

  visited = [0 for _ in range(n+1)]
  visited[start] = 1

  cnt = 1
  
  while q:
    s = q.popleft()

    for i in graph[s]:
      if not visited[i]:
        visited[i] = 1
        q.append(i)
        cnt += 1

  return cnt

result = []
max_cnt = 0

for i in range(1, n+1):
  cnt = bfs(i)

  if cnt > max_cnt:
    max_cnt = cnt
  result.append([i, cnt])

for i, cnt in result:
  if cnt == max_cnt:
    print(i, end=' ')
```
