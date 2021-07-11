# 🌼 Algorithm (Python) 🌼

[◾ 파이썬 주요 라이브러리](https://github.com/jinyand/Python_Algorithm/wiki/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%A3%BC%EC%9A%94-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC)  
[◾ DFS/BFS](https://github.com/jinyand/Python_Algorithm#-dfsbfs)  
[◾ 정렬](https://github.com/jinyand/Python_Algorithm#-%EC%A0%95%EB%A0%AC)  
[◾ 이진 탐색](https://github.com/jinyand/Python_Algorithm#-%EC%9D%B4%EC%A7%84-%ED%83%90%EC%83%89)  
[◾ 다이나믹 프로그래밍](https://github.com/jinyand/Python_Algorithm/blob/main/README.md#-%EB%8B%A4%EC%9D%B4%EB%82%98%EB%AF%B9-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D)


## 🔍 DFS/BFS
- 그래프의 기본 구조
    - 그래프는 노드와 간선으로 표현되며, 이때 노드 = 정점
    - 그래프 탐색이란 하나의 노드를 시작으로 다수의 노드를 방문하는 것
    - 두 노드가 간선으로 연결되어 있다면 = '두 노드는 인접하다'
    
- 그래프는 크게 2가지 방식으로 표현할 수 있다.
    - 인접 행렬 : 2차원 배열로 그래프의 연결 관계를 표현하는 방식
        - 2차원 리스트로 구현
        - 연결이 되어있지 않은 노드끼리는 무한의 비용이라고 작성 (999999999  등 값으로 초기화)
    - 인접 리스트 : 리스트로 그래프의 연결 관계를 표현하는 방식
        - 2차원 리스트로 구현
- 두 방식의 차이?
    - 인접 행렬 방식은 모든 관계를 저장하므로 노드 개수가 많을 수록 메모리가 불필요하게 낭비되는 반면
    - 인접 리스트 방식은 연결된 정보만을 저장하기 때문에 메모리를 효율적으로 사용
    - 하지만 이와 같은 속성 때문에 인접 리스트 방식은 인접 행렬 방식에 비해 특정한 두 노드가 연결되어 있는지에 대한 정보를 얻는 속도가 느리다.

### ▶ DFS
- Depth-First Search, 깊이 우선 탐색이라고도 부르며, 그래프에서 깊은 부분을 우선적으로 탐색하는 알고리즘
- 특정한 경로로 탐색하다가 특정한 상황에서 최대한 깊숙이 들어가서 노드를 방문한 후, 다시 돌아가 다른 경로로 탐색하는 알고리즘
- 스택 자료구조를 이용한 구체적인 동작 과정
    1. 탐색 시작 노드를 스택에 삽입하고 방문 처리를 한다.
    2. 스택의 최상단 노드에 방문하지 않은 인접 노드가 있으면 그 인접 노드를 스택에 넣고 방문 처리를 한다. 방문하지 않은 인접 노드가 없으면 스택에서 최상단 노드를 꺼낸다.
    3. 2번의 과정을 더 이상 수행할 수 없을 때까지 반복한다.
- 일반적으로 인접한 노드 중에서 방문하지 않은 노드가 여러 개 있으면 번호가 낮은 순서부터 처리한다.
- 예제 소스코드

    ```python
    # DFS 메서드 정의
    def dfs(graph, v, visited):
      # 현재 노드를 방문 처리
      visited[v] = True
      print(v, end=' ')
      # 현재 노드와 연결된 다른 노드를 재귀적으로 방문
      for i in graph[v]:
        if not visited[i]:
          dfs(graph, i, visited)

    graph = [
      [],
      [2, 3, 8],
      [1, 7],
      [1, 4, 5],
      [3, 5],
      [3, 4],
      [7],
      [2, 6, 8],
      [1, 7]
    ]

    # 각 노드가 방문된 정보를 리스트 자료형으로 표현
    visited = [False] * 9

    dfs(graph, 1, visited)
    ```
    
### ▶ BFS

- Breadth-First Search, 너비 우선 탐색, 가까운 노드부터 탐색하는 알고리즘이다.
- 최대한 멀리 있는 노드를 우선으로 탐색하는 방식인 DFS와 정반대이다.
- BFS 구현에서는 선입선출 방식인 큐 자료구조를 이용하는 것이 정석이다.
- 큐 자료구조를 이용한 구체적인 동작 과정
    1. 탐색 시작 노드를 큐에 삽입하고 방문 처리를 한다.
    2. 큐에서 노드를 꺼내 해당 노드의 인접 노드 중에서 방문하지 않은 노드를 모두 큐에 삽입하고 방문 처리를 한다.
    3. 2번의 과정을 더 이상 수행할 수 없을 때까지 반복한다.
- deque 라이브러리를 사용
- 일반적인 경우 실제 수행 시간은 DFS 보다 좋은 편이다.
- 예제 소스코드

    ```python
    from collections import deque

    # BFS 메서드 정의
    def bfs(graph, start, visited):
      queue = deque([start])

      # 현재 노드 방문 처리
      visited[start] = True

      # 큐가 빌 때까지 반복
      while queue:
        # 큐에서 하나의 원소를 뽑아 출력
        v = queue.popleft()
        print(v, end = ' ')
        # 해당 원소와 연결된, 아직 방문하지 않은 원소들을 큐에 삽입
        for i in graph[v]:
          if not visited[i]:
            queue.append(i)
            visited[i] = True

    graph = [
      [],
      [2, 3, 8],
      [1, 7],
      [1, 4, 5],
      [3, 5],
      [3, 4],
      [7],
      [2, 6, 8],
      [1, 7]
    ]

    # 각 노드가 방문된 정보를 리스트 자료형으로 표현
    visited = [False] * 9

    bfs(graph, 1, visited)
    ```
    
<br>

## 🔍 정렬
### ▶ 선택 정렬

- 매번 '가장 작은 것을 선택'
- 무작위의 데이터가 있을 때 가장 작은 데이터를 선택해 맨 앞에 있는 데이터와 바꾸고, 그 다음 작은 데이터를 선택해 앞에서 두 번째 데이터와 바꾸는 과정 반복

```python
array = [7, 5, 9, 0, 3, 1, 6, 2, 4, 8]

for i in range(len(array)):
  min_index = i
  for j in range(i+1, len(array)):
    if array[min_index] > array[j]:
      min_index = j
  
  array[i], array[min_index] = array[min_index], array[i] # 스와프(swap)

print(array)
```

- 시간복잡도 : N + (N - 1) + (N - 2) + ... + 2 ⇒ N x (N + 1) / 2 ⇒ O(N^2)
- 정렬 중에서 비효율적이지만 특정 리스트에서 가장 작은 데이터를 찾을 때 자주 사용됨

### ▶ 삽입 정렬

- 특정한 데이터를 적절한 위치에 '삽입'
- 적절한 위치에 들어가기 이전에, 그 앞까지의 데이터는 이미 정렬되어 있다고 가정

```python
array = [7, 5, 9, 0, 3, 1, 6, 2, 4, 8]

for i in range(len(array)):
  for j in range(i, 0, -1): # i부터 0까지 감소하며 반복
    if array[j] < array[j-1]: # 한 칸씩 왼쪽으로 이동
      array[j], array[j-1] = array[j-1], array[j]
    else:
      break

print(array)
```

- 시간 복잡도 : O(N^2)
- 삽입 정렬은 현재 리스트의 데이터가 거의 정렬되어 있는 상태라면 매우 빠르게 동작, 최선의 경우 O(N)의 시간 복잡도.
- 따라서 거의 정렬되어 있는 상태로 입력이 주어지는 문제라면 삽입 정렬이 효과적

### ▶ 퀵 정렬

- 빠르고, 가장 많이 사용되는 알고리즘
- 기준을 설정한 다음 큰 수와 작은 수를 교환한 후 리스트를 반으로 나누는 방식으로 동작
- 피벗 : 큰 숫자와 작은 숫자를 교환할 때, 교환하기 위한 '기준'

- 호어 분할 방식 : 가장 대표적인 분할 방식
    - 리스트에서 첫 번째 데이터를 피벗으로 정한다.
    - 피벗을 설정한 뒤에는 왼쪽에서부터 피벗보다 큰 데이터를 찾고, 오른쪽에서부터 피벗보다 작은 데이터를 찾은 다음 두 데이터의 위치를 서로 교환한다.
    - 이 과정을 반복하다가, 찾는 값의 위치가 서로 엇갈린 경우 '작은 데이터'와 피벗의 위치를 서로 변경한다.
    - 그럼 피벗이 가운데로 온 상태로 분할 완료. 왼쪽은 피벗보다 작은 데이터들, 오른쪽은 피벗보다 큰 데이터들이 위치한다.
    - 양쪽으로 분할된 데이터들을 위와 같은 과정으로 반복하여 정렬한다.

**일반 퀵 정렬 소스코드**

```python
array = [5, 7, 9, 0, 3, 1, 6, 2, 4, 8]

def quick_sort(array, start, end):
  if start >= end: # 원소가 1개인 경우
    return
  pivot = start # 피벗 = 첫번째 원소
  left = start + 1
  right = end # 마지막 원소

  while left <= right:
    # 피벗보다 큰 데이터를 찾을 때까지 반복
    while left <= end and array[left] <= array[pivot]:
      left += 1
    while right > start and array[right] >= array[pivot]:
      right -= 1
    if left > right: # 엇갈렸다면 작은 데이터와 피벗을 교체
      array[right], array[pivot] = array[pivot], array[right]
    else:
      array[left], array[right] = array[right], array[left]

  # 분할 이후 왼쪽 부분과 오른쪽 부분에서 각각 다시 정렬 수행
  quick_sort(array, start, right-1)
  quick_sort(array, right+1, end)

quick_sort(array, 0, len(array)-1)
print(array)
```

**파이썬의 장점을 살린 퀵 정렬 소스코드**

```python
array = [5, 7, 9, 0, 3, 1, 6, 2, 4, 8]

def quick_sort(array):
  # 리스트가 하나 이하의 원소만을 담고 있다면 종료
  if len(array) <= 1:
    return array

  pivot = array[0] # 피벗은 첫번째 원소
  tail = array[1:] # 피벗을 제외한 리스트

  left_side = [x for x in tail if x <= pivot] # 분할된 왼쪽 부분
  right_side = [x for x in tail if x > pivot] # 분할된 오른쪽 부분

  # 분할 이후 왼쪽 부분과 오른쪽 부분에서 각각 정렬 수행
  # 전체 리스트 반환
  return quick_sort(left_side) + [pivot] + quick_sort(right_side)

print(quick_sort(array))
```

- 시간 복잡도 : O(NlogN)
- '이미 데이터가 정렬되어 있는 경우' 매우 느리게 동작

### ▶ 계수 정렬

- 특정한 조건이 부합할 때만 사용할 수 있지만 매우 빠른 정렬 알고리즘
- '데이터의 크기 범위가 제한되어 정수 형태로 표현할 수 있을 때'만 사용할 수 있다.
- 앞의 세 정렬(비교 기반의 정렬 알고리즘)과는 다름
- 별도의 리스트를 선언하고, 데이터를 하나씩 확인하며 데이터의 값과 동일한 인덱스의 데이터를 1씩 증가시킨다.
- 결과적으로 리스트에는 각 데이터가 몇 번 등장했는지 그 횟수가 기록된다. 따라서 리스트의 첫 번째 데이터부터 하나씩 그 값만큼 인덱스를 출력하면 된다.

```python
# 모든 원소의 값이 0보다 크거나 같다고 가정
array = [7, 5, 9, 0, 3, 1, 6, 2, 9, 1, 4, 8, 0, 5, 2]

# 모든 범위를 포함하는 리스트 선언(모든 값은 0으로 초기화)
count = [0] * (max(array) + 1)

for i in range(len(array)):
  count[array[i]] += 1 # 각 데이터에 해당하는 인덱스의 값 증가

for i in range(len(count)): # 리스트에 기록된 정렬 정보 확인
  for j in range(count[i]):
    print(i, end=' ')
```

- 시간 복잡도 : O(N + K)

### ▶ 파이썬의 정렬 라이브러리

- sorted(array)
- array.sort()
- sorted()나 sort()를 이용할 때에는 key 매개변수를 입력으로 받을 수 있다. key 값으로는 하나의 함수가 들어가야 하며 이는 정렬 기준이 된다.

    ```python
    array = [('바나나', 2), ('사과', 5), ('당근', 3)]

    def setting(data):
    	return data[1]

    result = sorted(array, key=setting)
    print(result)

    # [('바나나', 2), ('당근', 3), ('사과', 5)]
    # 두 번째 원소(숫자) 기준으로 정렬됨
    ```
    
<br>

## 🔍 이진 탐색
### ▶ 순차 탐색

- 리스트 안에 있는 특정한 데이터를 찾기 위해 앞에서부터 데이터를 하나씩 차례대로 확인하는 방법
- 데이터 정렬 여부와 상관없이 가장 앞에 있는 원소부터 하나씩 확인 = O(N)

```python
def sequential_search(n, target, array):
  for i in range(n):
    if array[i] == target:
      return i + 1 # 현재 위치 반환

print("생성할 원소 개수, 찾을 문자열 입력")
input_data = input().split()
n = int(input_data[0])
target = input_data[1]

print("앞서 적은 개수만큼의 문자열 입력")
array = input().split()

print(sequential_search(n, target, array))
```

### ▶ 이진 탐색

- 배열 내부의 데이터가 정렬되어 있어야만 사용할 수 있는 알고리즘
- 탐색하고자 하는 범위의 시작점, 끝점, 중간점 변수 3개를 사용한다.
- 찾으려는 데이터와 중간점 위치에 있는 데이터를 반복적으로 비교해서 원하는 데이터를 찾는다.
- 한 번 확인할 때마다 확인하는 원소의 개수가 절반씩 줄어듦 = O(logN)
1. 재귀 함수를 이용하는 방법

    ```python
    def binary_search(array, target, start, end):
      if start > end:
        return None
      mid = (start+end) // 2

      if array[mid] == target:
        return mid
      elif array[mid] > target:
        return binary_search(array, target, start, mid-1)
      else:
        return binary_search(array, target, mid+1, end)
      
    n, target = list(map(int, input().split()))
    array = list(map(int, input().split()))

    result = binary_search(array, target, 0, n-1)
    if result == None:
      print("원소가 존재하지 않습니다.")
    else:
      print(result + 1)
    ```

2. 반복문을 이용하는 방법

    ```python
    def binary_search(array, target, start, end):
      while start <= end:
        mid = (start+end) // 2

        if array[mid] == target:
          return mid
        elif array[mid] > target:
          end = mid - 1
        else:
          start = mid + 1
      return None
      
    n, target = list(map(int, input().split()))
    array = list(map(int, input().split()))

    result = binary_search(array, target, 0, n-1)
    if result == None:
      print("원소가 존재하지 않습니다.")
    else:
      print(result + 1)
    ```
### ▶ 트리 자료구조

- 트리 자료구조는 노드와 노드의 연결로 표현하며 여기에서 노드는 정보의 단위로서 어떠한 정보를 가지고 있는 개체이다.

- 그래프 자료구조의 일종으로 데이터베이스 시스템이나 파일 시스템과 같은 곳에서 많은 양의 데이터를 관리하기 위한 목적으로 사용한다.

- 특징
    - 트리는 부모 노드와 자식 노드의 관계로 표현된다.
    - 트리의 최상단 노드를 루트 노드라고 한다.
    - 트리의 최하단 노드를 단말 노드라고 한다.
    - 트리에서 일부를 떼어내도 트리 구조이며 이를 서브 트리라 한다.
    - 트리는 파일 시스템과 같이 계층적이고 정렬된 데이터를 다루기에 적합하다.

- 정리하자면, 큰 데이터를 처리하는 소프트웨어는 대부분 데이터를 트리 자료구조로 저장해서 이진 탐색과 같은 기법을 이용해 빠르게 탐색이 가능하다.


### ▶ 이진 탐색 트리

- 이진 탐색이 동작할 수 있도록 고안된, 효율적인 탐색이 가능한 자료구조
- 특징
    - 부모 노드보다 왼쪽 자식 노드가 작다.
    - 부모 노드보다 오른쪽 자식 노드가 크다.
    - 즉, 왼쪽 자식 노드 < 부모 노드 < 오른쪽 자식 노드 가 성립해야한다.

- 이진 탐색 문제에서 시간 초과를 피하는 방법
    - `input()` 대신에 `sys.stdin.readline().rstrip()` 사용
    - `rstrip()` 함수는 입력 후 엔터가 줄 바꿈 기호로 입력될 때 이 공백 문자를 제거하기 위해 필요하다.
    
<br>

## 🔍 다이나믹 프로그래밍
### ▶ 피보나치 수열
- 피보나치 수열은 이전 두 항의 합을 현재의 항으로 설정하는 특징이 있는 수열
- 점화식 : 인접한 항들 사이의 관계식

```python
def fibo(x):
	if x == 1 or x == 2:
		return 1
	return fibo(x-1) + fibo(x-2)

print(fibo(4))
```

- f(n) 함수에서 n이 커질수록 수행 시간이 기하급수적으로 늘어난다. = O(2^N)

### ▶ 다이나믹 프로그래밍

조건 1. 큰 문제를 작은 문제로 나눌 수 있다.

조건 2. 작은 문제에서 구한 정답은 그것을 포함하는 큰 문제에서도 동일하다.

- 탑다운 방식 : 재귀 함수를 이용하여 다이나믹 프로그래밍 소스코드를 작성하는 방법, 큰 문제를 해결하기 위해 작은 문제를 호출한다.
- 메모이제이션 기법 : 다이나믹 프로그래밍을 구현하는 방법 중 한 종류, 한 번 구한 결과를 메모리 공간에 메모해두고 같은 식을 다시 호출하면 메모한 결과를 그대로 가져오는 기법 ( = 캐싱)

    ```python
    # 한 번 계산된 결과를 메모이제이션하기 위한 리스트 초기화
    d = [0] * 100

    def fibo(x):
      # 종료 조건 (1 or 2일 때 1을 반환)
      if x == 1 or x == 2:
        return 1
      
      # 이미 계산한 적 있는 문제라면 그대로 반환
      if d[x] != 0:
        return d[x]

      # 아직 계산한 적 없는 문제라면 점화식에 따라 반환
      d[x] = fibo(x-1) + fibo(x-2)
      return d[x]

    print(fibo(99))
    ```

- 보텀업 방식 : 반복문을 이용하여 소스코드를 작성하는 방법, 작은 문제부터 차근차근 답을 도출한다. (전형적인 방식)

    ```python
    d = [0] * 100

    d[1] = 1
    d[2] = 1
    n = 99

    for i in range(3, n+1):
      d[i] = d[i-1] + d[i-2]

    print(d[n])
    ```
    
<br>

## 🔍 최단 경로
### ▶ 다익스트라 최단 경로 알고리즘

- 그래프에서 여러 개의 노드가 있을 때, 특정한 노드에서 출발하여 다른 노드로 가는 각각의 최단 경로를 구해주는 알고리즘
- '음의 간선'이 없을 때 정상적으로 동작한다. 음의 간선 : 0보다 작은 값을 가지는 간선
- 그리디 알고리즘으로 분류 - '가장 비용이 적은 노드'를 선택해서 임의의 과정을 반복
- 원리
    1. 출발 노드를 설정한다.
    2. 최단 거리 테이블을 초기화한다.
    3. 방문하지 않은 노드 중에서 최단 거리가 가장 짧은 노드를 선택한다.
    4. 해당 노드를 거쳐 다른 노드로 가는 비용을 계산하여 최단 거리 테이블을 갱신한다.
    5. 위 과정에서 3과 4번을 반복한다.
- 특징 : '각 노드에 대한 현재까지의 최단 거리' 정보를 항상 1차원 리스트에 저장하며 리스트를 계속 갱신 = 최단 거리 테이블

- 매번 현재 처리하고 있는 노드를 기준으로 주변 간선을 확인

### ▶ 간단한 다익스트라 알고리즘

- 시간 복잡도 : O(V^2) (V = 노드의 개수)
- 단계마다 '방문하지 않은 노드 중에서 최단 거리가 가장 짧은 노드를 선택'하기 위해 매 단계마다 1차원 리스트의 모든 원소를 확인(순차 탐색)

```python
import sys
input = sys.stdin.readline
INF = int(1e9)

n, m = map(int, input().split()) # 노드, 간선
start = int(input()) # 시작 노드 번호
# 각 노드에 연결되어 있는 노드에 대한 정보
graph = [[] for i in range(n+1)]
# 방문 여부 리스트
visited = [False] * (n+1)
# 최단 거리 테이블 무한으로 초기화
distance = [INF] * (n+1)

# 모든 간선 정보 입력받기
for i in range(m):
  a, b, c = map(int, input().split())
  # a번 노드에서 b번 노드로 가는 비용이 c라는 의미
  graph[a].append((b, c))

# 방문하지 않은 노드 중에서, 가장 최단 거리가 짧은 노드의 번호를 반환
def get_smallest_node():
  min_value = INF
  index = 0 # 가장 최단 거리가 짧은 노드(인덱스)

  for i in range(1, n+1):
    if distance[i] < min_value and not visited[i]:
      index = i

  return index

def dijkstra(start):
  distance[start] = 0
  visited[start] = True

  for j in graph[start]:
    distance[j[0]] = j[1]

  # 시작 노드 제외한 전체 n-1개의 노드에 대해 반복
  for i in range(n-1):
    # 현재 최단 거리가 가장 짧은 노드를 꺼내서 방문 처리
    now = get_smallest_node()
    visited[now] = True

    # 현재 노드와 연결된 다른 노드를 확인
    for j in graph[now]:
      cost = distance[now] + j[1]
      # 현재 노드를 거쳐서 다른 노드로 이동하는 거리가 더 짧은 경우
      if cost < distance[j[0]]:
        distance[j[0]] = cost

dijkstra(start)

# 모든 노드로 가기 위한 최단 거리를 출력
for i in range(1, n+1):
  # 도달할 수 없는 경우, 무한(INF)이라고 출력
  if distance[i] == INF:
    print("INF")
  else:
    print(distance[i])
```

### ▶ 개선된 다익스트라 알고리즘

- 시간 복잡도 : O(ElogV) (V : 노드의 개수, E : 간선의 개수)
- 힙 자료구조 사용 - 특정 노드까지의 최단 거리에 대한 정보를 힙에 담아서 처리하므로 출발 노드로부터 가장 거리가 짧은 노드를 더욱 빠르게 찾을 수 있다.

    **힙 자료구조**

    - 우선순위 큐를 구현하기 위하여 사용하는 자료구조 중 하나
    - 우선순위 큐 : 우선순위가 가장 높은 데이터를 가장 먼저 삭제 / PriorityQueue & **heapq**
- 현재 가장 가까운 노드를 저장하기 위한 목적으로만 우선순위 큐를 추가로 이용
- 앞의 코드와 비교했을 때 get_smallest_node() 함수 작성할 필요 없음
- '최단 거리가 가장 짧은 노드'를 선택하는 과정을 다익스트라 최단 경로 함수 안에서 우선순위 큐를 이용하는 방식으로 대체

```python
import heapq
import sys
input = sys.stdin.readline
INF = int(1e9)

n, m = map(int, input().split()) # 노드, 간선
start = int(input()) # 시작 노드 번호
# 각 노드에 연결되어 있는 노드에 대한 정보
graph = [[] for i in range(n+1)]
# 방문 여부 리스트
visited = [False] * (n+1)
# 최단 거리 테이블 무한으로 초기화
distance = [INF] * (n+1)

# 모든 간선 정보 입력받기
for i in range(m):
  a, b, c = map(int, input().split())
  # a번 노드에서 b번 노드로 가는 비용이 c라는 의미
  graph[a].append((b, c))

def dijkstra(start):
  q = []
  # 시작 노드로 가기 위한 최단 경로는 0으로 설정, 큐에 삽입
  heapq.heappush(q, (0, start))
  distance[start] = 0
  while q: # 큐가 비어있지 않다면
    # 가장 최단 거리가 짧은 노드에 대한 정보 꺼내기
    dist, now = heapq.heappop(q)

    # 현재 노드가 이미 처리된 적이 있는 노드라면 무시
    if distance[now] < dist:
      continue

    # 현재 노드와 연결된 다른 인접 노드 확인
    for i in graph[now]:
      cost = dist + i[1]
      if cost < distance[i[0]]:
        distance[i[0]] = cost
        heapq.heappush(q, (cost, i[0]))

dijkstra(start)

# 모든 노드로 가기 위한 최단 거리를 출력
for i in range(1, n+1):
  # 도달할 수 없는 경우, 무한(INF)이라고 출력
  if distance[i] == INF:
    print("INF")
  else:
    print(distance[i])
```
