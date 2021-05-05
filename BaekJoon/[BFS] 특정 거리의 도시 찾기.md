# [BFS] 특정 거리의 도시 찾기

- 2021-05-05
- p.339

```python
from collections import deque

n, m, k, x = map(int, input().split())
graph = [[] for _ in range(n+1)]

for i in range(m):
  a, b = map(int, input().split())
  graph[a].append(b)

# 모든 도시에 대한 최단 거리 초기화
distance = [-1] * (n+1)
distance[x] = 0 # 출발 도시 ~ 출발 도시 최단거리 = 0
  
queue = deque([x])
while queue:
  now = queue.popleft()

  # 현재 도시와 연결된 도시들 확인
  for next in graph[now]:
    if distance[next] == -1:
      distance[next] = distance[now] + 1
      queue.append(next)

check = False
for i in range(1, n+1):
  if distance[i] == k:
    print(i)
    check = True

if check == False:
  print(-1)
```

- 문제에서 모든 도로의 거리는 1이다. = 모든 간선의 비용이 1이다.
- **모든 간선의 비용이 동일할 때는 너비 우선 탐색 BFS를 이용하여 최단 거리를 찾을 수 있다.**
- 특정 도시 x를 시작으로 BFS를 수행하여 모든 도시까지의 최단 거리를 계산한 뒤, 각 최단 거리를 하나씩 확인하여 k와 동일하면 해당 도시의 번호 출력
- check 변수 = 최단거리가 k인 도시가 있는지 없는지 확인 ⇒ 없으면 -1 출력
