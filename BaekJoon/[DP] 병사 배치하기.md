# [DP] 병사 배치하기

- 2021-07-10
- 18353번

```python
n = int(input())
array = list(map(int, input().split()))
# 뒤집어서 '가장 긴 증가하는 부분 수열' 문제로 변환
array.reverse()

dp = [1] * n

for i in range(1, n):
  for j in range(0, i):
    if array[j] < array[i]:
      dp[i] = max(dp[i], dp[j]+1)

print(n-max(dp))
```

- 가장 긴 증가하는 부분 수열 : 하나의 수열이 주어졌을 때 값들이 증사하는 형태의 가장 긴 부분 수열
- D[i] = array[i]를 마지막 원소로 가지는 부분 수열의 최대 길이
- 점화식 : 모든 0 ≤ j < i 에 대하여, D[i] = max(D[i], D[j] + 1) if array[j] < array[i]
