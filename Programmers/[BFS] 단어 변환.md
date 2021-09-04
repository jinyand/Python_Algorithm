# [BFS] 단어 변환

- 2021-09-04

```python
from collections import deque

def compare_word(begin, target):
    count = 0
    
    for i in range(len(begin)):
        if begin[i] != target[i]:
            count += 1
    
    if count == 1:
        return True
    else:
        return False

def solution(begin, target, words):
    answer = 0
    
    if target not in words:
        return 0
    
    q = deque()
    q.append((begin, 0))
    
    visited = [0] * len(words)
    
    while q:
        current = q.popleft()
        
        if current[0] == target:
            answer = current[1]
        
        for i in range(len(words)):
            if compare_word(current[0], words[i]) and visited[i] == 0:
                q.append((words[i], current[1] + 1))
                visited[i] = 1
                
        
    return answer
```

- 큐에 (현재 단어, 누적 변환 횟수) 형태로 넣어서 비교작업 반복
