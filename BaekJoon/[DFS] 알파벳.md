# [DFS] 알파벳

- 2022-01-24

```python
r, c = map(int, input().split())
# map을 이용해 자른 문자를 람다식을 활용하여 아스키코드로 바로 변환
# 알파벳이 숫자 형태로 board 배열에 저장됨
# visited 에서 방문 여부를 확인하기 편리
board = [list(map(lambda x: ord(x)-65, input().rstrip())) for _ in range(r)]
print(board)
visited = [0] * 26
result = 0

dx = [-1, 0, 1, 0]
dy = [0, -1, 0, 1]

def dfs(x, y, count):
  global result
  result = max(result, count)

  for i in range(4):
    nx = x + dx[i]
    ny = y + dy[i]

    if 0 <= nx < r and 0 <= ny < c:
      if not visited[board[nx][ny]]:
        visited[board[nx][ny]] = 1
        dfs(nx, ny, count+1)
        visited[board[nx][ny]] = 0
        # 백트래킹 - dfs에서 빠져나온 경우 (최대칸 수가 아닌 경우) 다시 되돌려줌

visited[board[0][0]] = 1
dfs(0, 0, 1)
print(result)
```
