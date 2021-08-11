# [BFS] 가장 먼 노드

- 2021-08-11

```python
from collections import deque

def solution(n, edge):
    answer = 0
    graph = [[] for _ in range(n+1)]
    
    for a, b in edge:
        graph[a].append(b)
        graph[b].append(a)
        
    distance = [-1] * (n+1)
    distance[1] = 0
    
    q = deque([1])
    
    while q:
        now = q.popleft()
        
        for next in graph[now]:
            if distance[next] == -1:
                distance[next] = distance[now] + 1
                q.append(next)
    
    
    for i in distance:
        if i == max(distance):
            answer += 1
    
    
    return answer
```
