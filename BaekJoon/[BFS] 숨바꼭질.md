# [BFS] 숨바꼭질

- 2021-05-12
- 1697번

```python
from collections import deque

n, k = map(int, input().split())
time = [0] * 100001

def bfs():
  q = deque()
  q.append(n)

  while q:
    temp = q.popleft()
    
    if temp == k:
      print(time[temp])
      return
    
    # 3가지 모두 연산
    for next in (temp-1, temp+1, temp*2):
      if 0 <= next < 100001 and time[next] == 0:
        time[next] = time[temp] + 1
        q.append(next)
    
bfs()
```

- for 구문에서 변수 3개를 사용하여 3가지 경우를 모두 연산한 뒤, 처음 도달하는 수라면 (`time[next] == 0`) 큐에 추가
- 각 연산으로 파생된 수(`time[next]`)는 이전의 수(`time[temp]`) 에서 1을 더하여 시간을 카운트 해준다.
