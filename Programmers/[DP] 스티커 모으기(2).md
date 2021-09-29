# [DP] 스티커 모으기(2)

- 2021-09-29

```python
def solution(sticker):
    answer = 0

    if len(sticker) == 1:
        return sticker[0]
    
    # 첫번째 스티커를 뜯는 경우 -> 맨 마지막 스티커 제외 (n)
    dp = [0 for i in range(len(sticker))]
    # dp 시작을 둘 다 첫번째 스티커 값으로 시작
    dp[0] = sticker[0]
    dp[1] = dp[0]
    
    for i in range(2, len(sticker)-1):
        dp[i] = max(dp[i-1], dp[i-2] + sticker[i])
    
    first = max(dp)
    
    # 첫번째 스티커를 뜯지않는 경우 -> 맨 마지막 스티커 포함 (n)
    dp = [0 for i in range(len(sticker))]
    dp[0] = 0 # 첫번째 스티커 사용 x
    dp[1] = sticker[1]
    
    for i in range(2, len(sticker)):
        dp[i] = max(dp[i-1], dp[i-2] + sticker[i])

    second = max(dp)
    
    answer = max(first, second)
    
    return answer
```
