# 🌼 Algorithm (Python) 🌼

[🎈 파이썬 주요 라이브러리](https://github.com/jinyand/Python_Algorithm/wiki/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%A3%BC%EC%9A%94-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC)

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
