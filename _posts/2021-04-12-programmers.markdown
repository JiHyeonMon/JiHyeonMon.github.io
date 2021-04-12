---
layout: post
title: "프로그래머스 코딩테스트"
date: 2021-04-12 23:59 +0530
categories: python
---

알고리즘 풀기 99일차

:)

- # 가장 먼 노드

# < 문제 >

n개의 노드가 있는 그래프가 있습니다. 각 노드는 1부터 n까지 번호가 적혀있습니다. 1번 노드에서 가장 멀리 떨어진 노드의 갯수를 구하려고 합니다. 가장 멀리 떨어진 노드란 최단경로로 이동했을 때 간선의 개수가 가장 많은 노드들을 의미합니다.

노드의 개수 n, 간선에 대한 정보가 담긴 2차원 배열 vertex가 매개변수로 주어질 때, 1번 노드로부터 가장 멀리 떨어진 노드가 몇 개인지를 return 하도록 solution 함수를 작성해주세요.

![image](https://user-images.githubusercontent.com/50662636/114182936-3475da80-997e-11eb-96e6-6ebb1959405f.png)

# < 제한사항 >

노드의 개수 n은 2 이상 20,000 이하입니다.

간선은 양방향이며 총 1개 이상 50,000개 이하의 간선이 있습니다.

vertex 배열 각 행 [a, b]는 a번 노드와 b번 노드 사이에 간선이 있다는 의미입니다.

# < 풀이 >

```python

def solution(n, edge):
     answer = 0

     # 이중 배열의 안의 배열 정렬
     for i in range(len(edge)):
          edge[i] = sorted(edge[i])
     # 이중 배열의 바깥 배열 정렬
     edge = sorted(edge)

     # 엣지 개수 만큼 0 채운 배열 만듬
     num = [0 for i in range(n)]

     d = []
     for i in range(len(edge)):
          if edge[i][0] == 1:
               d[edge[i][1]] = 1

     for i in range(len(edge)):
          if d[edge[i][1]] != 0:
               continue
          else:
               d[edge[i][1]] = d[edge[i][0]]

     print(d)


     return answer

n = 6
edge = [[3, 6], [4, 3], [3, 2], [1, 3], [1, 2], [2, 4], [5, 2]]
solution(n, edge)

```

사실 아직 푸는 중.........

> 1 ) edge = [[3, 6], [4, 3], [3, 2], [1, 3], [1, 2], [2, 4], [5, 2]]

> 2 ) 이중 배열 안의 정렬

> 2 ) edge = [[3, 6], [3, 4], [2, 3], [1, 3], [1, 2], [2, 4], [2, 5]]

> 3 ) 배열 정렬

> 3 ) edge = [[1, 2], [1, 3], [2, 3], [2, 4], [2, 5], [3, 4], [3, 6]]

여기서 n길이의 0으로 찬 배열을 만들어서 해당 노드에 가중치? 거리를 더해주려고 한다.

n = [ 0, 0, 0, 0, 0, 0]

[1, 2], [1, 3]이니 d에 2, 3번째 자리에 가중치 1

n = [0, 1, 1, 0, 0, 0]

이런 식으로 생각만~~~

---

```python

import collections

def solution(n, edge):
    answer = 0

    # 이중 배열의 안의 배열 정렬
    for i in range(len(edge)):
        edge[i] = sorted(edge[i])
    # 이중 배열의 바깥 배열 정렬
    edge = sorted(edge)

    # 시간 효율성 위해 deque로 구현
    edge = collections.deque(edge)

    # 엣지 개수 만큼 0 채운 배열 만듬
    num = [0] * n

    i = 0
    while edge:
        i+=1
        tmp = edge.popleft()
        if num[tmp[1]-1] == 0:
            num[tmp[1]-1] = num[tmp[0]-1] + 1
        else:
            continue

    return num.count(max(num))

n = 6
edge = [[3, 6], [4, 3], [3, 2], [1, 3], [1, 2], [2, 4], [5, 2]]
solution(n, edge)

```

두번째 시도

테스트는 통과, 그러나 안통과,,,,,,,,,,

해당 아래 예시는 통과한다,,,^^ 더 수정 필요

우선 위의 풀이에서 수정한게 정렬 후 Queue로 만들어 넣는다. 그래서 하나하나 앞에서부터 값을 빼면서 num에 거리를 계산해서 넣어준다.