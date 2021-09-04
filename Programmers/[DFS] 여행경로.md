# [DFS] 여행경로

- 2021-09-05

```python
from collections import defaultdict

def solution(tickets):
    answer = []
    
    ticket_list = defaultdict(list)
    
    for ticket in tickets:
        ticket_list[ticket[0]].append(ticket[1])
        
    for key in ticket_list:
        ticket_list[key].sort()
    
    route = ["ICN"]
    
    while route:
        current = route[-1]
        
        # 현재 위치에서 갈 수 있는 경로가 있을 경우
        if current in ticket_list and ticket_list[current]:
            route.append(ticket_list[current].pop(0))
        # 현재 위치에서 경로가 끊긴 경우
        else:
            answer.append(route.pop())

    answer.reverse()
    
    return answer
```

- 길이 중간에 끊어지면 안되기 때문에 오름차순으로 진행하면 중간에 길이 끊어질 수도 있다.
- 따라서 마지막 노드부터 거꾸로 넣어주는 방식을 사용
    1. 현재 위치에서 갈 수 있는 경로가 있을 경우 ⇒ 스택에 넣어준다.  
        → 스택의 마지막 원소(가장 최근에 추가한 원소)를 꺼내어 같은 작업 반복
    2. 현재 위치에서 갈 수 있는 경로 없이 끊긴 경우 ⇒ answer에 넣어준다.
- 거꾸로 넣어주었기 때문에 역순으로 출력
