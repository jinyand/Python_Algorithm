# [DFS, BFS] 타겟 넘버

- 2021-08-03

```python
from collections import deque

def solution(numbers, target):
    answer = 0
    
    q = deque()
    q.append([numbers[0], 0])
    q.append([-numbers[0], 0])
    
    while q:
        temp, idx = q.popleft()
        idx += 1
        if idx < len(numbers):
            q.append([temp+numbers[idx], idx])
            q.append([temp-numbers[idx], idx])
        else:
            if temp == target:
                answer += 1
        
    return answer
```

- 그래프 문제인 이유
    - 1 → 2 → 3, 1 → ...
    - 1 → 0 → 1, -1 → ...
    - 위와 같이 다음 인덱스에 해당하는 numbers원소를 더하거나 뺀 값을 방문하기 때문
- numbers의 길이만큼 연산을 반복한 뒤 최종적으로 deque에 들어있는 값 중 target과 일치하는 값을 카운트한다.
