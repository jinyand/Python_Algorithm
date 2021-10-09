# [BFS] 촌수계산

- 2021-10-09

```python
from collections import deque

n = int(input())
p1, p2 = map(int, input().split())

m = int(input())
arr = [[] for i in range(n+1)]
result = [0 for i in range(n+1)]

for i in range(m):
  x, y = map(int, input().split())
  arr[x].append(y)
  arr[y].append(x)

def bfs(start):
  q = deque()
  q.append(start)
  visited = [False] * (n+1)
  visited[start] = True

  while q:
    s = q.popleft()
    for i in arr[s]:
      if not visited[i]:
        visited[i] = True
        result[i] = result[s] + 1
        q.append(i)

bfs(p1)

if result[p2] != 0:
  print(result[p2])
else:
  print(-1)
```

- 입력받은 첫번째 촌수를 기준으로 연결되어 있는 사람의 촌수를 + 1
