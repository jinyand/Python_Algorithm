# [DP] 퇴사

- 2021-07-09
- 14501번

```python
n = int(input())
t = [] # 기간
p = [] # 금액
dp = [0] * (n+1)
max_value = 0

for _ in range(n):
  x, y = map(int, input().split())
  t.append(x)
  p.append(y)

for i in range(n-1, -1, -1):
  time = t[i] + i

  # 상담이 기간 안에 끝나는 경우
  if time <= n:
    dp[i] = max(dp[time] + p[i], max_value)
    max_value = dp[i]
  else:
    dp[i] = max_value

print(max_value)
```

- 뒤쪽부터 거꾸로 확인하는 방식으로 뒤쪽 dp[i] 값을 미리 구하고 앞쪽 dp[i]에서 이를 활용
- dp[i] = i번째 날부터 마지막 날까지 낼 수 있는 최대 이익
