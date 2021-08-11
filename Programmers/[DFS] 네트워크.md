# [DFS] 네트워크

- 2021-08-11

```python
def solution(n, computers):
    
    answer = 0
    visited = [False] * n
    
    def dfs(i):
        visited[i] = True
        for a in range(n):
            if computers[i][a] and not visited[a]:
                dfs(a)
    
    for i in range(n):
        if not visited[i]:
            dfs(i)
            answer += 1
    
    return answer
```
