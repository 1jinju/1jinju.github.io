---
layout: post
title: Lv.1 시저 암호
subtitle: 프로그래머스
cover-img: /assets/img/black.jpg
thumbnail-img: https://korenainthekitchen.com/wp-content/uploads/2011/02/white.jpg
share-img: /assets/img/path.jpg
tags: [Python, 프로그래머스]
---

[시저 암호](https://school.programmers.co.kr/learn/courses/30/lessons/12926)

**문제 설명**

어떤 문장의 각 알파벳을 일정한 거리만큼 밀어서 다른 알파벳으로 바꾸는 암호화 방식을 시저 암호라고 합니다. 예를 들어 "AB"는 1만큼 밀면 "BC"가 되고, 3만큼 밀면 "DE"가 됩니다. "z"는 1만큼 밀면 "a"가 됩니다. 문자열 s와 거리 n을 입력받아 s를 n만큼 민 암호문을 만드는 함수, solution을 완성해 보세요.

 

**제한 조건**
- 공백은 아무리 밀어도 공백입니다.
- s는 알파벳 소문자, 대문자, 공백으로만 이루어져 있습니다.
- s의 길이는 8000이하입니다.
- n은 1 이상, 25이하인 자연수입니다.
 

**입출력 예**

|s	|n	|result|
|---|---|---|
|"AB"|1	|"BC"|
|"z"|1	|"a"|
|"a B z"|4	|"e F d"|

<br><br>

---

# 나의 풀이
```python
def solution(s, n):
    answer = ''
    for i in range(len(s)):
        if s[i:i+1] == ' ':
            answer += ' '
        else:
            a = ord(s[i:i+1]) + n
            if a > 122 or (a > 90 and s[i:i+1].isupper()):
                a -= 26
            answer += chr(a)
    return answer
```
문자열을 하나씩 인덱스 슬라이싱을 이용하여 하나씩 자른다.


공백이면 answer에 공백을 추가하고,<br>
공백이 아니면 자른 문자열을 아스키 코드로 바꾼(ord 함수 이용) 후 n을 더한 값을 변수 a에 넣는다.<br>


a가 122보다 크거나(a>'z')<br>
a가 90보다 크고(a>'Z') 대문자이면,<br>
a에 26을 빼준다.<br>
-> 이유: `만약 s가 'z'이고 n이 3이라면, answer는 'c'이어야 한다. 그런데 a는 125이므로 answer는 아스키 코드에서 125에 해당되는 '}'이 된다. 따라서, 알파벳이 나오도록 26을 빼주어야 한다.`

 

a를 다시 알파벳으로 바꾸어주고(chr 함수 이용) return 해준다.<br>
이 과정을 문자열의 길이만큼 반복한다.

<br>

# 다른 사람의 풀이
```python
def caesar(s, n):
    s = list(s)
    for i in range(len(s)):
        if s[i].isupper():
            s[i]=chr((ord(s[i])-ord('A')+ n)%26+ord('A'))
        elif s[i].islower():
            s[i]=chr((ord(s[i])-ord('a')+ n)%26+ord('a'))

    return "".join(s)
```
s에서 대문자인 경우와 소문자인 경우를 나눠서 계산한다.


s[i]가 공백인지 아닌지 굳이 확인할 필요가 없다는 것을 알게 되었다.<br>
s는 알파벳 소문자, 대문자, 공백으로만 이루어져 있으니까...<br>
앞으로는 문제 조건을 잘 읽어야겠다!<br>
 

확실히 내 코드보다 더 깔끔하고 이해하기 쉬운 것 같다.<br><br>