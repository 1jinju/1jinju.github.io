---
layout: post
title: Lv.1 콜라츠 추측
subtitle: 프로그래머스
cover-img: /assets/img/black.jpg
thumbnail-img: https://korenainthekitchen.com/wp-content/uploads/2011/02/white.jpg
share-img: /assets/img/path.jpg
tags: [Python, 프로그래머스]
---

[콜라츠 추측](https://school.programmers.co.kr/learn/courses/30/lessons/12943)

**문제 설명**

1937년 Collatz란 사람에 의해 제기된 이 추측은, 주어진 수가 1이 될때까지 다음 작업을 반복하면, 모든 수를 1로 만들 수 있다는 추측입니다. 작업은 다음과 같습니다.

```
1-1. 입력된 수가 짝수라면 2로 나눕니다. 
1-2. 입력된 수가 홀수라면 3을 곱하고 1을 더합니다.
2. 결과로 나온 수에 같은 작업을 1이 될 때까지 반복합니다.
```
예를 들어, 입력된 수가 6이라면 6→3→10→5→16→8→4→2→1 이 되어 총 8번 만에 1이 됩니다. 위 작업을 몇 번이나 반복해야하는지 반환하는 함수, solution을 완성해 주세요. 단, 작업을 500번을 반복해도 1이 되지 않는다면 –1을 반환해 주세요.

 

**제한 사항**

- 입력된 수, num은 1 이상 8000000 미만인 정수입니다.
 

**입출력 예**

|n	|result|
|---|---|
|6	|8|
|16	|4|
|626331|	-1|
 
**입출력 예 설명**  
`입출력 예 #1`  
문제의 설명과 같습니다.

`입출력 예 #2`  
16 -> 8 -> 4 -> 2 -> 1 이되어 총 4번만에 1이 됩니다.

`입출력 예 #3`  
626331은 500번을 시도해도 1이 되지 못하므로 -1을 리턴해야합니다.

<br>

---

# 나의 풀이
```python
def solution(num):
    answer = 0
    while num != 1:
        if num % 2 == 0:
            num /= 2
        else:
            num = num * 3 + 1
        answer += 1
        if answer == 500:
            return -1
    return answer
```
조건에 맞게 짝수이면 2로 나눠주고, 홀수이면 3을 곱한 후 1을 더해주는 작업을 num이 1이 될 때까지 반복하였다.<br>
while 문을 반복하다가 answer이 500이 되면 -1을 return해준다.<br>

<br>

# 다른 사람의 풀이
```python
def collatz(num):
    for i in range(500):
    	if num == 1:
            return i
        num = num / 2 if num % 2 == 0 else num*3 + 1   
    return -1
```
for 문을 통해 500번 반복하는데, num이 1이면 i를 return하고 그렇지 않으면 위의 작업을 해주는 식이다.<br>
500번 반복이 끝나도 1이 되지 않으면 -1을 return해준다.<br>
 
<br>

```python
def collatz(num):
    for i in range(500):
        num = num / 2 if num % 2 == 0 else num*3 + 1
        if num == 1:
            return i + 1
    return -1
```
이게 원래 코드였는데 i+1을 return하는 게 별로인 것 같아서 if 문을 위로 올려 i를 return하게 하였다.

<br>
