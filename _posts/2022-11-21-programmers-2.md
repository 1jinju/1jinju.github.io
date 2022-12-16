---
layout: post
title: Lv.2 가장 큰 수
subtitle: 프로그래머스
cover-img: /assets/img/black.jpg
thumbnail-img: https://korenainthekitchen.com/wp-content/uploads/2011/02/white.jpg
share-img: /assets/img/path.jpg
tags: [Python, 프로그래머스]
---
[가장 큰 수](https://school.programmers.co.kr/learn/courses/30/lessons/42746)

**문제 설명**

0 또는 양의 정수가 주어졌을 때, 정수를 이어 붙여 만들 수 있는 가장 큰 수를 알아내 주세요.

예를 들어, 주어진 정수가 [6, 10, 2]라면 [6102, 6210, 1062, 1026, 2610, 2106]를 만들 수 있고, 이중 가장 큰 수는 6210입니다.

 

0 또는 양의 정수가 담긴 배열 numbers가 매개변수로 주어질 때, 순서를 재배치하여 만들 수 있는 가장 큰 수를 문자열로 바꾸어 return 하도록 solution 함수를 작성해주세요.

 

**제한 사항**

- numbers의 길이는 1 이상 100,000 이하입니다.
- numbers의 원소는 0 이상 1,000 이하입니다.
- 정답이 너무 클 수 있으니 문자열로 바꾸어 return 합니다.
 

**입출력 예**

|numbers	|return|
|---|---|
|[6, 10, 2]	|"6210"|
|[3, 30, 34, 5, 9]	|"9534330"|

<br>

---

# 나의 풀이
```python
def solution(numbers):
    answer = ''
    l=[]
    largest=0
    x=0
    k=len(numbers)
    if sum(numbers)==0:
        return 0
    while k>0:
        for i in numbers:
            while(i>=10):
                i//=10
            l.append(i%10)
        for j in range(len(l)):    
            if largest<l[j]:
                largest=l[j]
                x=j
            elif largest==l[j]:
                lst2=[str(numbers[j]),str(numbers[x])]
                lst3=[str(numbers[x]),str(numbers[j])]
                a=''.join(lst2)
                b=''.join(lst3)
                if a>b:
                    largest=l[j]
                    x=j
        answer+=str(numbers[x])
        del numbers[x]
        k=k-1
        l=[]
        largest=0
        x=0
    return answer
```
`실패(시간초과)`<br>
for 문에 while 문까지 중첩되어 있으니 시간초과가 난 것 같다.<br>
시간을 줄일 수 있는 방법이 있다면 이 풀이방법도 나쁘지 않은 것 같다.<br>

 

// l: numbers의 첫 번째 자릿수가 들어가 있는 리스트<br>
// largest: 리스트 l 중에 가장 큰 수<br>
// x: 리스트 l 중에 가장 큰 수의 인덱스<br>

 

numbers가 0으로만 이루어져 있을 경우 return 값이 000...이 되므로 numbers의 합이 0이면 '0'을 반환한다.<br>


numbers에서 첫 번째 자릿수만을 뽑아 리스트 l에 넣는다.<br>


리스트 l에서 가장 큰 수를 찾는데, 가장 큰 수가 여러 개일 경우 현재 인덱스의 numbers 값과 largest일 때 인덱스의 numbers 값을 붙여 큰 값을 찾는다.<br>
예를 들어, 해당되는 numbers가 각각 '34', '30' 이라면, '3430'과 '3034'를 비교하여 큰 값을 찾는다.<br>
for 문을 다 돌고나면 리스트 l 중 가장 큰 수가 largest에 저장된다.<br>


answer에 문자열로 변환한 numbers 값을 더해준다.<br>
반환값에 더해주었으니 numbers에서는 삭제한다.<br>


위의 과정을 numbers의 길이만큼 반복한다.<br>

<br>

# 다른 사람의 풀이
```python
def solution(numbers):
    numbers = list(map(str, numbers))
    numbers.sort(key=lambda x: x*3, reverse=True)
    return str(int(''.join(numbers)))
```
numbers에 map을 사용하여 문자열로 변환한 리스트를 넣어준다.<br>
문자열 리스트 numbers를 앞의 세 자리만 비교하여 내림차순으로 정렬한다.<br>


예를 들어 numbers=[6, 2, 10]였다면, ['666', '222', '101']이 정렬되어 ['6', '10', '2']가 된다.<br>
이 리스트를 join을 사용해 하나로 합치고 반환한다.<br>


마지막 줄에서 합친 문자열을 int로 변환했다가 str로 다시 변환하는 이유는 numbers가 0으로만 이루어져 있을 경우 return 값이 000...이 되기 때문에 이를 막기 위해서이다.<br>


lambda 생각해내기 너무 어렵다!<br>


<br>