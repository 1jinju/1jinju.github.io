---
layout: post
title: Lv.1 하샤드 수
subtitle: 프로그래머스
cover-img: /assets/img/black.jpg
thumbnail-img: https://korenainthekitchen.com/wp-content/uploads/2011/02/white.jpg
share-img: /assets/img/path.jpg
tags: [Python, 프로그래머스]
---

[하샤드 수](https://school.programmers.co.kr/learn/courses/30/lessons/12947)

**문제 설명**

양의 정수 x가 하샤드 수이려면 x의 자릿수의 합으로 x가 나누어져야 합니다. 예를 들어 18의 자릿수 합은 1+8=9이고, 18은 9로 나누어 떨어지므로 18은 하샤드 수입니다. 자연수 x를 입력받아 x가 하샤드 수인지 아닌지 검사하는 함수, solution을 완성해주세요.

 

**제한 조건**

- x는 1 이상, 10000 이하인 정수입니다.
 
**입출력 예**

|x	|return|
|---|---|
|10	|true|
|12	|true|
|11	|false|
|13	|false|
 
**입출력 예 설명**  
`입출력 예 #1`<br>
10의 모든 자릿수의 합은 1입니다. 10은 1로 나누어 떨어지므로 10은 하샤드 수입니다.<br>

`입출력 예 #2`<br>
12의 모든 자릿수의 합은 3입니다. 12는 3으로 나누어 떨어지므로 12는 하샤드 수입니다.<br>

`입출력 예 #3`<br>
11의 모든 자릿수의 합은 2입니다. 11은 2로 나누어 떨어지지 않으므로 11는 하샤드 수가 아닙니다.<br>

`입출력 예 #4`<br>
13의 모든 자릿수의 합은 4입니다. 13은 4로 나누어 떨어지지 않으므로 13은 하샤드 수가 아닙니다.

<br>

---

# 나의 풀이
```python
def solution(x):
    if x % sum(int(i) for i in str(x)) == 0:
        return True
    else:
        return False
```
x를 str(x)로 바꿔주고 for 문을 통해 각자리 수를 다시 int로 바꿔준 후 sum() 함수를 통해 더해준다.<br>
x를 앞의 값과 나눠주어 나머지가 0이면 True(1)를 반환, 0이 아니면 False(0)을 반환한다.<br>
 

처음엔 if x % sum(int(i) for i in x) == 0: 으로 풀었다.<br>
그랬더니 `TypeError: 'int' object is not iterable`가 떠서 x 대신 str(x)를 넣어주었다.<br>


정수의 각자릿수를 리스트에 넣어 더해주는 방식으로 풀 수도 있다.<br>
위와 같은 방법이긴 하다.<br>

```python
def solution(x):
    l = list(map(int, str(x))
    if x % sum(l) ==0:
        return True
    else:
        return False
```

<br> 

# 다른 사람의 풀이
```python
def Harshad(n):
    return n % sum([int(c) for c in str(n)]) == 0
```
내가 푼 것과 유사하나 if 문을 사용하지 않은 풀이이다.<br>
1이 True이고 0이 False이므로 x가 하샤드 수냐 아니냐에 따라 결과가 나오게 하였다.<br>


sum 함수를 쓰는 것에만 집중하느라 코드를 간결히 하는 것에 신경쓰지 못한 것 같다.<br>
사실 리스트의 값을 더할 때 또 for 문이 생각나긴 했다 ^^..<br>

<br>

