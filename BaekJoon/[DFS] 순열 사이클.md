# [DFS] 순열 사이클

- 2022-01-18

```python
t = int(input())

def dfs(num):
  visited[num] = True
  next_num = numbers[num]
  if not visited[next_num]:
    dfs(next_num)

for i in range(t):
  n = int(input())
  numbers = [0] + list(map(int, input().split()))
  visited = [True] + [False] * n
  result = 0

  for i in range(1, n+1):
    if not visited[i]:
      dfs(i)
      result += 1

  print(result)
```

- dfs를 통해 그래프를 순회하며 싸이클의 개수 확인
