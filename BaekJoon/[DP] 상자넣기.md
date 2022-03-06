# [DP] 상자넣기

- 2022-03-06

```python
n = int(input())
box = list(map(int, input().split()))
dp = []
dp.append(1)

for i in range(1, n):
  d = [] # i와 (i-i) ~ (i-1) 까지 비교한 결과

  for j in range(i):
    if box[i] > box[j]:
      d.append(dp[j] + 1)

  if not d: # d가 비어있으면 1로 초기화
    dp.append(1)
  else:
    dp.append(max(d))

print(max(dp))
```
