---
layout: post
title: Lv.1 부족한 금액 계산하기
subtitle: 프로그래머스
cover-img: /assets/img/black.jpg
thumbnail-img: https://korenainthekitchen.com/wp-content/uploads/2011/02/white.jpg
share-img: /assets/img/path.jpg
tags: [Python, 프로그래머스]
---

[부족한 금액 계산하기](https://school.programmers.co.kr/learn/courses/30/lessons/82612)

**문제 설명**

새로 생긴 놀이기구는 인기가 매우 많아 줄이 끊이질 않습니다. 이 놀이기구의 원래 이용료는 price원 인데, 놀이기구를 N 번 째 이용한다면 원래 이용료의 N배를 받기로 하였습니다. 즉, 처음 이용료가 100이었다면 2번째에는 200, 3번째에는 300으로 요금이 인상됩니다.

놀이기구를 count번 타게 되면 현재 자신이 가지고 있는 금액에서 얼마가 모자라는지를 return 하도록 solution 함수를 완성하세요.
단, 금액이 부족하지 않으면 0을 return 하세요.

 

**제한 사항**
- 놀이기구의 이용료 price : 1 ≤ price ≤ 2,500, price는 자연수
- 처음 가지고 있던 금액 money : 1 ≤ money ≤ 1,000,000,000, money는 자연수
- 놀이기구의 이용 횟수 count : 1 ≤ count ≤ 2,500, count는 자연수
 

**입출력 예**

|price	|money	|count	|result|
|---|---|---|---|
|3	|20	|4	|10|
 

**입출력 예 설명**

`입출력 예 #1`

이용금액이 3인 놀이기구를 4번 타고 싶은 고객이 현재 가진 금액이 20이라면, 총 필요한 놀이기구의 이용 금액은 30 (= 3+6+9+12) 이 되어 10만큼 부족하므로 10을 return 합니다.

<br>

---

# 나의 풀이

```python
def solution(price, money, count):
    sum = 0
    for i in range(1, count+1):
        sum += i * price
    if sum - money <= 0:
        return 0
    return sum-money
``` 

// sum: 놀이기구를 타기 위해 필요한 금액

 

놀이기구를 count번 타기 위해 필요한 금액을 1부터 하나씩 증가해가며 price와 곱한 후 sum에 더해준다.
 

sum-money가 0보다 작거나 같으면 금액이 부족하지 않은 것이므로 0을 return해준다.<br>
그렇지 않으면 sum-money(부족한 금액)을 return해준다.

<br>

# 다른 사람의 풀이

```python
def solution(price, money, count):
    return max(0,price*(count+1)*count//2-money)
```
등차수열의 합 공식을 이용해서 푼 풀이이다.


1+ ... +count = count*(count+1)/2이므로 price와 곱한 값에서 money를 빼주면 부족한 금액이 나온다.<br>
만약 금액이 부족하지 않으면 money를 뺀 값이 음수이므로 큰 값인 0이 return 된다.<br>
금액이 부족하다면 money를 뺀 값이 양수이므로 money를 뺀 값이 return 된다.<br>
 

수학적으로 풀 수도 있구나...<br>
감탄이 나오는 풀이이다.

<br>
