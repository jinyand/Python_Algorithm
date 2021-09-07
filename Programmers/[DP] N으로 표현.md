# [DP] N으로 표현

- 2021-09-07

```python
def solution(N, number):
    answer = 0
    
    # 조합으로 나올 수 있는 숫자들 set
    possible_set = [0, [N]]
    
    if N == number:
        return 1
    
    for i in range(2, 9):
        # i 별로 set을 만들어서 possible set에 추가
        # {N}, {NN}, {NNN} ...
        case_set = []
        N_num = int(str(N)*i)
        case_set.append(N_num)
        
        for j in range(1, i//2+1):
            for x in possible_set[j]:
                for y in possible_set[i-j]:
                    case_set.append(x+y)
                    case_set.append(x-y)
                    case_set.append(y-x)
                    case_set.append(x*y)
                    if y:
                        case_set.append(x//y)
                    if x:
                        case_set.append(y//x)
        
        if number in case_set:
            return i
        
        possible_set.append(case_set)
            
    return -1
```

- N을 3개 써야하는 경우 ⇒ N을 1개 써야하는 경우와 N을 2개 써야하는 경우끼리 연산하여 구할 수 있다.
- 따라서 set를 [N], [NN], [NNN] ... 으로 구성한 뒤 연산
- 두번째 for문 범위를 1부터 i//2 까지 설정한 이유는 절반 이상으로 넘어가면 같은 결과가 나오기 때문
    - ex) 3 = 2 + 1 = 1 + 2
    - 이렇게 설정한 대신 연산 부분에서 y-x, y//x 처럼 거꾸로 연산도 수행해주어야 한다.
