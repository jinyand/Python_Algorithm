# [DFS] 연산자 끼워 넣기

- 2021-05-11
- p.349

```python
n = int(input())
data = list(map(int, input().split()))
add, sub, mul, div = map(int, input().split())

min_value = 1e9
max_value = -1e9

def dfs(i, now):
  global min_value, max_value, add, sub, mul, div

  # 모든 수 연산 끝
  if i == n:
    min_value = min(now, min_value)
    max_value = max(now, max_value)

  else:
    if add > 0:
      add -= 1
      dfs(i+1, now+data[i])
      add += 1
    if sub > 0:
      sub -= 1
      dfs(i+1, now-data[i])
      sub += 1
    if mul > 0:
      mul -= 1
      dfs(i+1, now*data[i])
      mul += 1
    if div > 0:
      div -= 1
      dfs(i+1, int(now/data[i]))
      div += 1

dfs(1, data[0])

print(max_value)
print(min_value)
```

- 각 연산자에 대하여 재귀적으로 완전 탐색 후, 각 연산에 대해 최솟값과 최댓값을 출력
