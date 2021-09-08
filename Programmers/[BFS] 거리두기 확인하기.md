# [BFS] 거리두기 확인하기

- 2021-09-08

```python
from collections import deque

def bfs(place, idx):
    q = deque([idx])
    moves = [[-1, 0], [1, 0], [0, -1], [0, 1]]
    visited = [[False] * 5 for _ in range(5)]
    
    while q:
        x, y, c = q.popleft()
        visited[x][y] = True
        
        for move in moves:
            nx = x + move[0]
            ny = y + move[1]
            nc = c + 1
            
            if 0 <= nx < 5 and 0 <= ny < 5 and not visited[nx][ny]:
                visited[nx][ny] = True
                
                if place[nx][ny] == 'P':
                    if nc <= 2:
                        return 0
                elif place[nx][ny] == 'O':
                    if nc == 1:
                        q.append([nx, ny, nc])
                            
    return 1

    
def solution(places):
    answer = []
    
    for place in places:
        flag = 1
        
        # 거리두기 확인
        for i in range(5):
            for j in range(5):
                if place[i][j] == 'P':
                    if not bfs(place, [i, j, 0]):
                        flag = 0
    
        answer.append(flag)

    return answer
```
