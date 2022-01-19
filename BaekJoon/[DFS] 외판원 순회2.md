# [DFS] 외판원 순회2

- 2022-01-19

```python
import sys

input = sys.stdin.readline
n = int(input())
w = [list(map(int, input().split())) for i in range(n)]
min_value = sys.maxsize

def dfs(cur, total_value):
  global min_value

  # 최솟값이 아닌 경우 바로 return 하여 실행 시간 줄임
  if total_value > min_value:
    return

  # 다시 출발 도시로 돌아왔을 때
  if cur == k and visited[k] == 2:
    for v in visited:
      if v == 0: # 방문하지 않은 도시가 있다면 return
        return
    min_value = min(total_value, min_value)
    return

  for i in range(n):
    # 다시 출발 도시로 가는 경우
    if w[cur][i] != 0 and i == k:
      visited[i] += 1
      dfs(i, total_value + w[cur][i])
      visited[i] -= 1

    # 해당 도시의 비용이 0이 아니고,
    # 아직 방문하지 않은 도시로 가는 경우
    if w[cur][i] != 0 and not visited[i]:
      visited[i] += 1
      dfs(i, total_value + w[cur][i])
      visited[i] -= 1

for k in range(n):
  visited = [0] * n
  visited[k] = 1 # 모든 도시에서 시작 = i
  dfs(k, 0) # 출발 도시, 비용

print(min_value)
```
