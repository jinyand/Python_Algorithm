# [BFS] 퍼즐

- 2022-01-23

```python
from collections import deque

def bfs(start):
  q = deque()
  q.append(start)
  visited[start] = 0

  while q:
    v = q.popleft()

    if v == '123456780':
      return visited[v]

    s = str(v)
    target = s.find('0') # 0의 인덱스

    tx = target // 3
    ty = target % 3

    # ex) target == 7인 경우
    # tx = 2, ty = 1
    # 좌표 = (2, 1)

    for i in range(4):
      nx = tx + dx[i]
      ny = ty + dy[i]

      if 0 <= nx < 3 and 0 <= ny < 3:
        next_s = list(s) # 위치교환을 위한 리스트 변환
        next_idx = nx * 3 + ny # 다음 target의 인덱스

        # 위치 교환
        next_s[target], next_s[next_idx] = next_s[next_idx], next_s[target]

        # 다시 문자열로 변환
        next_s = ''.join(next_s)

        # 방문 딕셔너리에 추가
        if not visited.get(next_s):
          visited[next_s] = visited[v] + 1
          q.append(next_s)

  return -1

dx = [-1, 0, 1, 0]
dy = [0, -1, 0, 1]

# 딕셔너리 {현재 퍼즐 문자열 : 퍼즐 이동횟수}
visited = dict()

start = '' # 시작 문자열
for i in range(3):
  start += ''.join(list(input().split()))

print(bfs(start))
```

- 방문 여부를 표시하기 위해 {현재 퍼즐 문자열 : 퍼즐 이동횟수} 형태의 딕셔너리 사용
