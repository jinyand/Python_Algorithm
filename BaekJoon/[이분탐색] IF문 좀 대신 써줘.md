# [이분탐색] IF문 좀 대신 써줘

- 2022-03-01

```python
import sys
input = sys.stdin.readline

n, m = map(int, input().split())
graph = [list(input().split()) for _ in range(n)]

def binary_search(graph, num):
  start, end = 0, len(graph)-1
  result = 0

  while start <= end:
    mid = (start + end) // 2

    if int(graph[mid][1]) >= num:
      end = mid - 1
      result = mid
    else:
      start = mid + 1
  return result

for _ in range(m):
  num = int(input())
  b = binary_search(graph, num)
  print(graph[b][0])
```

- if 문을 이분탐색으로 대신해서 사용
- 이분탐색으로 쓰는 이유 : 칭호의 개수가 10만개 나올 수 있으니 완전 탐색으로 찾을 때 최악의 경우 10만 * 10만 ⇒ 시간초과
- 이분탐색 알고리즘이 한 번 도는데 시간복잡도가 logN이므로, 최악의 경우 NlogN 번 내에 모든 경우를 다 찾을 수 있기 때문
- 따라서 이분탐색으로 자신보다 크거나 같은 수 중에 가장 작은 수를 찾으면 된다.
