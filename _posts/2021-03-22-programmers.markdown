---
layout: post
title:  "프로그래머스 코딩테스트"
date:   2021-03-22 23:59 +0530
categories: python
---

알고리즘 풀기 90일차

:)

- # 124 나라의 숫자

# < 문제 >

124 나라가 있습니다. 124 나라에서는 10진법이 아닌 다음과 같은 자신들만의 규칙으로 수를 표현합니다.

124 나라에는 자연수만 존재합니다.
124 나라에는 모든 수를 표현할 때 1, 2, 4만 사용합니다.
예를 들어서 124 나라에서 사용하는 숫자는 다음과 같이 변환됩니다.


10진법	    124 나라	    0진법	     124 나라
1	        1	            6	        14
2	        2	            7   	    21
3	        4	            8	        22
4	        11	            9	        24
5	        12	            10	        41

자연수 n이 매개변수로 주어질 때, n을 124 나라에서 사용하는 숫자로 바꾼 값을 return 하도록 solution 함수를 완성해 주세요.

# < 제한사항 >

n은 500,000,000이하의 자연수 입니다.

# < 풀이 >

```python

def solution(n):
    answer = ''
    if n > 3:
        while n > 3:
            if n%3 == 1:
                answer += "1"
                n = n//3
            elif n%3 == 2:
                answer += "2"
                n = n//3
            else:
                answer += "4"
                n = n//3 -1
                
    if n == 3:
        answer+="4"
    else:
        answer+=str(n)
        
    return answer[::-1]

```

규칙을 적어나가다 보니 찾은 규칙. 

- 우선 1,2,4만 쓰이니 3개 단위로 쪼갤 수 있음. 1로 나눠 떨어지면 끝자리 1, 2로 나눠 떨어지면 끝자리 2, 3으로 나눠 떨어지면 끝자리 4

- 그러고 3을 나눠준다. (반복) - 3보다 작은 경우, 마지막에 한번 더 처리

- 계속 answer에 더해준다. (그러나 사실 반대로 앞자리가 바껴야하는 것)

- 그래서 출력은 반대로 해준다.

---

첫번째로 reverse 안해줘서 오류
두번째로는 3으로 나눠떨어질 경우 -1 해주는 거 못찾아서 오류

세번만에 통과

나름 선방했다고 생각한다.

