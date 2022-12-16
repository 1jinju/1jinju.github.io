---
layout: post
title: Lv.1 두 정수 사이의 합
subtitle: 프로그래머스
cover-img: /assets/img/black.jpg
thumbnail-img: https://korenainthekitchen.com/wp-content/uploads/2011/02/white.jpg
share-img: /assets/img/path.jpg
tags: [Python, 프로그래머스]
---

[Lv.1 두 정수 사이의 합](https://school.programmers.co.kr/learn/courses/30/lessons/12912)

**문제 설명**

두 정수 a, b가 주어졌을 때 a와 b 사이에 속한 모든 정수의 합을 리턴하는 함수, solution을 완성하세요.<br>
예를 들어 a = 3, b = 5인 경우, 3 + 4 + 5 = 12이므로 12를 리턴합니다.

 
**제한 조건**

- a와 b가 같은 경우는 둘 중 아무 수나 리턴하세요.
- a와 b는 -10,000,000 이상 10,000,000 이하인 정수입니다.
- a와 b의 대소관계는 정해져있지 않습니다.
 

**입출력 예**

|a	|b	|return|
|---|---|---|
|3	|5	|12|
|3	|3|	3|
|5	|3|	12|

<br>

---

# 나의 풀이
```python
def solution(a, b):
    answer = 0
    if a == b:
        return a
    elif a > b:
        for i in range(b, a+1):
            answer += i
        return answer
    else:
        for i in range(a, b+1):
            answer += i
        return answer
```
설명하지 않아도 될 정도로 쉽게 풀었지만.. 설명해보자면!<br>
문제 조건에 맞춰 `(1) a와 b가 같은 경우`, `(2) a가 b보다 큰 경우`, `(3) a가 b보다 작은 경우`로 나누어 풀었다.


`(1) a와 b가 같은 경우` a를 return한다.<br>
`(2) a가 b보다 큰 경우` b부터 a까지 answer에 더한 값을 return한다.<br>
`(3) a가 b보다 작은 경우` a부터 b까지 answer에 더한 값을 return한다.<br>

<br>

# 다른 사람의 풀이
```python
def adder(a, b):
    return (abs(a-b)+1)*(a+b)//2
```
저번에 내가 풀었던 '부족한 금액 계산하기' 문제처럼 n(n+1)/2를 이용해서 푼 풀이이다.

![Untitle](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdrI9GE%2Fbtrvas0l3ne%2FjSOeGCwVFscGxry24K1KNk%2Fimg.jpg)

바로 이렇게 풀었다고 하면 자괴감 들 것 같은데<br>
앞으로 다른 사람의 풀이를 바로 보지 않고 더 좋은 풀이는 없나 생각해보는 시간을 가져야겠다.<br>
적어도 다른 풀이 하나는 생각하기!<br>

 

```python
def adder(a, b):
    if a > b: a, b = b, a
    
    return sum(range(a,b+1))
```
if문을 이용해 a에 둘 중 작은 수를 넣고 a부터 b까지 더해주어 푼 풀이이다.


파이썬에 sum, abs, max 함수 등 정말 많은 함수가 존재하는데 내가 왜 안 쓰고 있는 건지 모르겠다.<br>
sum 함수면 되는데 for 문으로 푼 걸 깨닫고 많이 반성했다.<br>
for 문 멈추고 함수 쓰자!<br>

<br>
