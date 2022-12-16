---
layout: post
title: Lv.1 실패율
subtitle: 프로그래머스
cover-img: /assets/img/black.jpg
thumbnail-img: https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FZAhE9%2FbtrqujnSTSj%2FkN5zBG4lNebtRD9IJXTBA1%2Fimg.png
share-img: /assets/img/path.jpg
tags: [Python, 프로그래머스]
---

[2019 KAKAO BLIND RECRUITMENT](https://school.programmers.co.kr/learn/courses/30/lessons/42889)

![Untitile](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FZAhE9%2FbtrqujnSTSj%2FkN5zBG4lNebtRD9IJXTBA1%2Fimg.png)

**문제 설명**  

슈퍼 게임 개발자 오렐리는 큰 고민에 빠졌다. 그녀가 만든 프랜즈 오천성이 대성공을 거뒀지만, 요즘 신규 사용자의 수가 급감한 것이다. 원인은 신규 사용자와 기존 사용자 사이에 스테이지 차이가 너무 큰 것이 문제였다.  

이 문제를 어떻게 할까 고민 한 그녀는 동적으로 게임 시간을 늘려서 난이도를 조절하기로 했다. 역시 슈퍼 개발자라 대부분의 로직은 쉽게 구현했지만, 실패율을 구하는 부분에서 위기에 빠지고 말았다. 오렐리를 위해 실패율을 구하는 코드를 완성하라.

- 실패율은 다음과 같이 정의한다.
    - 스테이지에 도달했으나 아직 클리어하지 못한 플레이어의 수 / 스테이지에 도달한 플레이어 수

전체 스테이지의 개수 N, 게임을 이용하는 사용자가 현재 멈춰있는 스테이지의 번호가 담긴 배열 stages가 매개변수로 주어질 때, 실패율이 높은 스테이지부터 내림차순으로 스테이지의 번호가 담겨있는 배열을 return 하도록 solution 함수를 완성하라.


**제한사항**

- 스테이지의 개수 N은 1 이상 500 이하의 자연수이다.
- stages의 길이는 1 이상 200,000 이하이다.
- stages에는 1 이상 N + 1 이하의 자연수가 담겨있다.
    - 각 자연수는 사용자가 현재 도전 중인 스테이지의 번호를 나타낸다.
    - 단, N + 1 은 마지막 스테이지(N 번째 스테이지) 까지 클리어 한 사용자를 나타낸다.
- 만약 실패율이 같은 스테이지가 있다면 작은 번호의 스테이지가 먼저 오도록 하면 된다.
- 스테이지에 도달한 유저가 없는 경우 해당 스테이지의 실패율은 0 으로 정의한다.
 

**입출력 예**

|N	|stages	                 |result     |
|---|---|---|
|5	|[2, 1, 2, 6, 2, 4, 3, 3]|[3,4,2,1,5]|
|4	|[4,4,4,4,4]             |[4,1,2,3]  |
 

**입출력 예 설명**

 

`입출력 예 #1`


1번 스테이지에는 총 8명의 사용자가 도전했으며, 이 중 1명의 사용자가 아직 클리어하지 못했다. 따라서 1번 스테이지의 실패율은 다음과 같다.

- 1 번 스테이지 실패율 : 1/8

2번 스테이지에는 총 7명의 사용자가 도전했으며, 이 중 3명의 사용자가 아직 클리어하지 못했다. 따라서 2번 스테이지의 실패율은 다음과 같다.

- 2 번 스테이지 실패율 : 3/7

마찬가지로 나머지 스테이지의 실패율은 다음과 같다.

- 3 번 스테이지 실패율 : 2/4
- 4번 스테이지 실패율 : 1/2
- 5번 스테이지 실패율 : 0/1

각 스테이지의 번호를 실패율의 내림차순으로 정렬하면 다음과 같다.

- [3,4,2,1,5]
 

`입출력 예 #2`

 

모든 사용자가 마지막 스테이지에 있으므로 4번 스테이지의 실패율은 1이며 나머지 스테이지의 실패율은 0이다.

- [4,1,2,3]


---

# 나의 풀이

![나의 풀이](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcgEcYs%2FbtrqujOWR7E%2F5hgvnJux8WPQQoBszoGyQk%2Fimg.png)

*answer: return 되는 리스트*<br>
*lst: 실패율 리스트*<br>
*p: 스테이지에 도달한 플레이어 수* <br>
*new_lst: lst를 내림차순으로 정렬한 리스트*<br>

​
1번 스테이지의 실패율은 stages에서의 1의 개수/전체 이용자 수이다.<br>
여기서 전체 이용자 수는 stages의 길이와 같으므로 초기 p값에 stages의 길이를 넣어준다.


1부터 N번까지 lst에 각 스테이지의 실패율을 넣는 연산을 반복한다.<br>
p는 실패율의 분모이므로 0이 되어서는 안 된다.<br>
p가 0일 때는 lst에 0을 넣어주고 p가 0이 아닐 때는 실패율을 계산하여 lst에 넣어준다.


for 문을 거치고 나면 lst엔 스테이지의 번호 순대로 저장되어 있는 실패율이 담겨 있다.<br>
스테이지의 번호를 내림차순으로 return해야 하므로 `sorted()`를 사용하여 정렬해주었다.<br>
따로 설정하지 않으면 reverse=False(오름차순 정렬)가 동작하고 내림차순 정렬을 하려면 reverse=True로 설정해주어야 한다.<br>

​
이중 for 문에선 new_lst와 lst의 값들을 하나씩 비교하여 둘의 값이 같으면 answer에 스테이지의 번호를 넣어준다.<br>
<br>


# 다른 사람의 풀이

![다른 사람의 풀이](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FFQOE6%2FbtrqzRcDeKa%2FKQPo2tnG1I6E3w6m2zGopK%2Fimg.png)

여기서 그냥 break을 쓰면 다음 반복문에서 중복되어 계산될 수도 있으므로 실패율로 나올 수 없는 값인 2를 넣어준다.<br>
다른 사람의 풀이에서 가장 상단에 떠 있는 풀이를 가져왔다.<br>


이중 for 문 쓰고 싶지 않아서 리스트 안에 리스트를 넣는 방법은 없나 생각하다가 위처럼 푼 건데 ㅠㅠ<br>
딕셔너리의 존재를 그냥 잊어버리고 있었다. lambda도 처음 들어봤다...<br>
파이썬 따로 공부하지 않은 지가 꽤 됐는데 다시 공부 시작해야 될 것 같다.<br>

<br>