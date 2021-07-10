# [DP] 못생긴 수

- 2021-07-10

```python
n = int(input())

array = [0] * n
array[0] = 1

# 2, 3, 5배를 위한 인덱스
i2 = i3 = i5 = 0
next2, next3, next5 = 2, 3, 5

for i in range(1, n):
  array[i] = min(next2, next3, next5)

  if array[i] == next2:
    i2 += 1
    next2 = array[i2] * 2
  if array[i] == next3:
    i3 += 1
    next3 = array[i3] * 3
  if array[i] == next5:
    i5 += 1
    next5 = array[i5] * 5

print(array[n-1])
```

- array[i] = min(next2, next3, next5) 여기서 가장 작은 수를 배열에 넣고, 각 변수를 순차적으로 2, 3, 5배 연산해주면 정렬된 배열이 만들어짐
