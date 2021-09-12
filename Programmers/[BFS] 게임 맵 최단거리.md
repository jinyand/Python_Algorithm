# [BFS] 게임 맵 최단거리

- 2021-09-12

```python
from collections import deque

def solution(maps):
    answer = 0
    
    n = len(maps)
    m = len(maps[0])
    
    dx = [-1, 0, 1, 0]
    dy = [0, -1, 0, 1]
    
    q = deque()
    q.append((0, 0))
    
    while q:
        x, y = q.popleft()
        
        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]
            
            if 0 <= nx < n and 0 <= ny < m:
                if maps[nx][ny] == 1:
                    maps[nx][ny] += maps[x][y]
                    q.append((nx, ny))
        
        
    if maps[n-1][m-1] == 1:
        answer = -1
    else:
        answer = maps[n-1][m-1]
    
    
    return answer
```
