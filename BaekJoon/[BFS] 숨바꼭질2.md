# [BFS] 숨바꼭질2

- 2022-02-06

```python
import sys
from collections import deque
input = sys.stdin.readline

n, k = map(int, input().split())
q = deque()
q.append(n)
visited = [-1 for _ in range(100001)]
visited[n] = 0

while q:
  s = q.popleft()

  if s == k:
    print(visited[s])
    break

  if 0 <= s*2 < 100001 and visited[s*2] == -1:
    # 0초후 순간이동 = 방문 카운트 더하지 않음
    visited[s*2] = visited[s]
    q.append(s*2)
    
  if 0 <= s-1 < 100001 and visited[s-1] == -1:
    visited[s-1] = visited[s] + 1
    q.append(s-1)

  if 0 <= s+1 < 100001 and visited[s+1] == -1:
    visited[s+1] = visited[s] + 1
    q.append(s+1)
```

- 순간이동 시에는 방문 카운트가 되지 않으므로 if 문 순서를 잘 배치해줘야함
