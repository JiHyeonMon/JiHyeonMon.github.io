---
layout: post
title: "[프로그래머스] 2개 이하로 다른 비트"
date: 2021-05-18 23:33 +0530
categories: 프로그래머스 월간코드챌린지2
---

알고리즘 풀기 119일차

:)

- # 2개 이하로 다른 비트
  >

## < 문제 >

양의 정수 x에 대한 함수 f(x)를 다음과 같이 정의합니다.

    x보다 크고 x와 비트가 1~2개 다른 수들 중에서 제일 작은 수

예를 들어,

    f(2) = 3 입니다. 다음 표와 같이 2보다 큰 수들 중에서 비트가 다른 지점이 2개 이하이면서 제일 작은 수가 3이기 때문입니다.

|수| 비트| 다른 비트의 개수|
2| 000...0010| |
3| 000...0011| 1|

f(7) = 11 입니다. 다음 표와 같이 7보다 큰 수들 중에서 비트가 다른 지점이 2개 이하이면서 제일 작은 수가 11이기 때문입니다.

|수| |비트| 다른 비트의 개수|
|7| |000...0111| |
|8| |000...1000| 4|
|9| |000...1001| 3|
|10| |000...1010| 3|
|11| |000...1011| 2|

정수들이 담긴 배열 numbers가 매개변수로 주어집니다. numbers의 모든 수들에 대하여 각 수의 f 값을 배열에 차례대로 담아 return 하도록 solution 함수를 완성해주세요.

## < 풀이 >

```python

def smallbit(bit):
    if '0' in bit[1:]:
        cnt = 2
        for i in range(len(bit)-1, 0, -1):
            if cnt == 0:
                return int('0b'+bit, 2)

            if bit[i] == '0':
                bit = bit[:i]+'1'+bit[i+1:]
                cnt -= 1
        return int('0b'+bit, 2)
    else:
        return int('0b10'+bit[1:], 2)

def solution(numbers):
    answer = []
    for i in range(len(numbers)):
        answer.append(smallbit(bin(numbers[i]).replace('0b', '')))

    return answer


# 입력: [2,7]	-> 출력: [3,11]
```

풀기야 했는데 죄다 틀렸다 ㅎㅎㅎ

정말 예시 두개만 통과하고,, 문제를 간과했다.

우선 진법 계산은 파이썬 라이브러리를 이용했다. bin()을 이용해서 10진수를 2진수로 바꾸는데 이때 앞에 '0b'가 필수적으로 붙어 슬라이싱을 한 채로 계산에 들어갔다.

우선 경우는 두가지로 생각했다.

(맨 앞자리는 1이 당연) 뒤에 0이 있는가 없는가.

0이 있다면 젤 뒤에서부터 가까운 순으로 0 -> 1로 바꾸는게 최소값이 될 것이다.

0이 없다면 다 1. 그러면 당연 앞자리가 커질 수밖에 없다. 그럼 앞자리 1이 생기며 하나의 비트 바뀌고 나머지 하나의 비트 1 -> 0 바꾸면서 최소를 하려면 앞자리일 수록 좋기에 맨 자리를 10으로 바꿔주는 작업을 거쳤다.

---

다시 생각을 해야할 것 같다.

오늘 너무 피곤해서,,,,,ㅠㅠㅠㅠㅠㅠㅠㅠ 하나 진짜 풀고 잘랬는데, 내일 이 문제 하나와 다른 문제 하나 꼭 풀기,,,,,,풀기,,,,,,,,진짜,,,,,,,,,,
