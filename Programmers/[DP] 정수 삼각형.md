# [DP] 정수 삼각형

- 2021-09-01

```python
def solution(triangle):
    answer = 0
    
    arr = [[0] * len(triangle) for i in range(len(triangle))]
    arr[0][0] = triangle[0][0]
    
    # 양 끝에서 내려오는 수
    for i in range(1, len(triangle)):
        arr[i][0] = arr[i-1][0] + triangle[i][0]
        arr[i][i] = arr[i-1][i-1] + triangle[i][i]
        
    # 중간에서 내려오는 수 = 위에 있는 두 수 중 큰 값 비교 후 계산
    for i in range(2, len(triangle)):
        for j in range(1, i):
            arr[i][j] = max(arr[i-1][j-1], arr[i-1][j]) + triangle[i][j]
            
    answer = max(arr[-1])
    
    return answer
```
