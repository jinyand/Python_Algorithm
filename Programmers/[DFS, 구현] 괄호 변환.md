# [DFS, 구현] 괄호 변환

- 2021-05-09
- p.346

```python
# "올바른 괄호 문자열"인지 체크
def check(p):
    count = 0
    for i in p:
        if i == '(':
            count += 1
        else:
            if count == 0:
                return False
            count -= 1
            
    return True

# 2단계 - "균형잡힌 괄호 문자열" 분리
def seperate(p):
    count = 0
    for i in range(len(p)):
        if p[i] == '(':
            count += 1
        else:
            count -= 1
        if count == 0:
            return i
    
def solution(p):
    answer = ''
    
    if p == '':
        return answer
    
    index = seperate(p)
    u = p[:index+1]
    v = p[index+1:]
    
    # u가 "올바른 괄호 문자열"이면
    if check(u):
        answer = u + solution(v) # v에 대해 재귀적으로 수행
    else:
        # 4-1 ~ 4-3
        answer = '('
        answer += solution(v)
        answer += ')'
        
        u = list(u[1:-1]) # 4-4 첫번째와 마지막 문자 제거
        
        for i in range(len(u)):
            if u[i] == '(':
                u[i] = ')'
            else:
                u[i] = '('
                
        answer += "".join(u)
        
    return answer
```

- u 문자열의 첫번째와 마지막 문자를 제거하는 코드 `u = list(u[1:-1])`
- 2단계에서 문자열을 분리하기 위해 따로 함수를 만들어 index를 반환하니 훨씬 코드가 단순해졌다.
