# [BFS] DSLR

- 2022-01-22

```python
from collections import deque

t = int(input())

def bfs(a, b):
  q = deque()
  q.append((a, ""))
  visited = [False] * 10000

  while q:
    num, op = q.popleft()
    visited[num] = True

    if num == b:
      return op

    # D
    da = (num * 2) % 10000
    if not visited[da]:
      q.append((da, op+"D"))
      visited[da] = True
    
    # S
    sa = (num - 1) % 10000
    if not visited[sa]:
      q.append((sa, op+"S"))
      visited[sa] = True

    # L
    la = ((num * 10) + (num // 1000)) % 10000
    if not visited[la]:
      q.append((la, op+"L"))
      visited[la] = True

    # R
    ra = ((num // 10) + ((num % 10) * 1000)) % 10000
    if not visited[ra]:
      q.append((ra, op+"R"))
      visited[ra] = True

for _ in range(t):
  a, b = map(int, input().split())

  print(bfs(a, b))
```
