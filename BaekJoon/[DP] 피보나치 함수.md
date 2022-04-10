# [DP] 피보나치 함수

- 2022-04-10

```python
t = int(input())
for _ in range(t):
  # 재귀 : 시간초과
  # 0과 1의 규칙을 찾아서 문제 해결
  cnt_0 = [1, 0]
  cnt_1 = [0, 1]
  n = int(input())

  # 0의 개수 = 이전 1의 개수
  # 1의 개수 = 이전 0 + 이전 1의 개수
  if n > 1:
    for i in range(n-1):
      cnt_0.append(cnt_1[-1])
      cnt_1.append(cnt_0[-2] + cnt_1[-1])

  print(cnt_0[n], cnt_1[n])
```
