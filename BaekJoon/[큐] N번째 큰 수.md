# [큐] N번째 큰 수

- 2022-02-24

```python
import heapq
import sys
input = sys.stdin.readline

n = int(input())
q = []

for _ in range(n):
  nums = list(map(int, input().split()))

  if not q:
    for num in nums:
      heapq.heappush(q, num)
  else:
    for num in nums:
      if q[0] < num:
        heapq.heappop(q)
        heapq.heappush(q, num)

# N 길이 만큼의 큐를 유지하기 때문에
# 해당 큐의 0번째 값이 N번째 큰 수가 된다.
print(q[0])
```

- N 길이만큼의 우선순위 큐를 유지하는 것이 중요
