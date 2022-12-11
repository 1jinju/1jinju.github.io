---
layout: post
title: Ch 6. 스택
subtitle: 윤성우의 열혈 자료구조
cover-img: /assets/img/black.jpg
thumbnail-img: https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6f64bda0-10b2-4459-976b-1ddcd9a5dbf1/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T170007Z&X-Amz-Expires=86400&X-Amz-Signature=eec0a713636c1de05931238aec80488893d7f481861cbaf98217e820ea893278&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject
share-img: /assets/img/path.jpg
tags: [자료구조]
---

# 06-1 스택의 이해와 ADT 정의

## 스택의 이해

먼저 들어간 것이 나중에 나온다  
후입선출(LIFO, Last-In First-Out) 방식의 자료구조  
예) 쌓아 올려진 상자더미, 쟁반 위에 쌓인 접시  

<br>

## 스택 ADT의 정의

```python
def __init__(self): # 스택 초기화

def is_empty(self): # 스택이 빈 경우 True(1)를, 그렇지 않은 경우 False(0)를 반환

def push(self, item): # 스택에 데이터를 저장

def pop(self): # 마지막에 저장된 요소를 삭제하고 반환

def show(self): # 스택에 있는 데이터 보여줌
```

배열과 연결 리스트를 이용하여 구현할 수 있다.

<br>

---

# 06-2 스택의 배열 기반 구현

![배열 기반 구현](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6f64bda0-10b2-4459-976b-1ddcd9a5dbf1/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T170007Z&X-Amz-Expires=86400&X-Amz-Signature=eec0a713636c1de05931238aec80488893d7f481861cbaf98217e820ea893278&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

삽입과 삭제가 일어나는 끝은 Top, 반대편 끝은 Bottom

- push: Top을 위로 한 칸 올리고, Top이 가리키는 위치에 데이터 저장
- pop: Top이 가리키는 데이터를 반환하고, Top을 아래로 한 칸 내림

파이썬은 배열을 리스트로 제공함

```python
s = []
for i in range(5):
	s.append(i)
print(s)
print(s.pop())
print(s.pop())
print(s)
```

![실행 결과](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f0e5e931-db76-421a-a39c-7d2eade97065/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T170133Z&X-Amz-Expires=86400&X-Amz-Signature=1427a4a0453ba438b0093253be989d5841964a30c5f230609b540602e102cd7d&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

<br>

---

# 06-3 스택의 연결 리스트 기반 구현

![연결 리스트 기반 구현](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ec8852bc-569d-4980-8c36-2236fb2d5667/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T170228Z&X-Amz-Expires=86400&X-Amz-Signature=847479e783508d0e3baa816c383f0209d3e86979a1337605b04684520ef25f0f&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

```python
class Node:
    def __init__(self, item, next):
        self.item = item
        self.next = next

class Stack:
    def __init__(self):
        self.last = None

    def is_empty(self):
        if self.last == None:
            return True
        else:
            return False

    def push(self, item):
        self.last = Node(item, self.last)

    def pop(self):
        item = self.last.item
        self.last = self.last.next
        return item

    def show(self):
        if self.is_empty():
            print('스택 비어 있음')
        else:
            l=[]
            cur_node = self.last
            while cur_node.next is not None:
                l.append(cur_node.item)
                cur_node = cur_node.next
            l.append(cur_node.item)
            print(list(reversed(l)))

s = Stack()
for i in range(5):
    s.push(i)
s.show()
print(s.pop())
print(s.pop())
s.show()
```

![실행 결과](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1606a391-81f2-4bf4-a99d-770e1f689a41/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T170302Z&X-Amz-Expires=86400&X-Amz-Signature=46161c84ff7c59eab238ae37d94383c44f9addb71bf27a80e5a18053e8217796&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

<br>

---

# 06-4 계산기 프로그램 구현

## 수식의 표기법: 중위, 전위, 후위

중위 표기법(infix notation) 예) 5 + 2 / 7  
전위 표기법(prefix notation) 예) + 5 / 2 7  
후위 표기법(postfix notation) 예) 5 2 7 + /  

- 전위 표기법이나 후위 표기법의 수식은 연산자의 배치순서에 따라서 연산 순서가 결정됨  
    → 이 두 표기법의 수식을 계산하기 위해서 연산자의 우선순위를 알 필요가 없다.
- 소괄호도 삽입되지 않음  
    → 소괄호에 대한 처리도 불필요하다.
    

<aside>
💡 계산기 사용자가 중위 표기법의 수식을 입력하면 그 수식을 전위나 후위 표기법의 수식으로 변환

</aside>

<br>

## 중위 표기법을 후위 표기법으로 바꾸는 방법

1. 중위 표기법의 수식을 후위 표기법의 수식으로 바꾼다.
    1. 피연산자는 그냥 옮긴다.
    2. 연산자는 스택으로 옮긴다.
    3. 연산자가 스택에 있다면 우선순위를 비교하여 처리방법을 결정한다.
        1. 스택에 위치한 연산자의 우선순위가 높다면, 스택의 연산자를 거내 변환된 수식이 위치한 자리로 옮긴다. 새 연산자는 스택으로 옮긴다.
        2. 스택에 위치한 연산자의 우선순위가 낮다면, 스택에 위치한 연산자의 위에 새 연산자를 쌓는다.
        3. ( 연산자는 ) 연산자가 등장할 때까지 쟁반에 남아서 소괄호의 경계를 구분하는 도구로 사용되어야 한다. ( 연산자의 우선순위는 어떤 사칙 연산자들보다 낮다.
    4. 마지막까지 스택에 남아있는 연산자들은 하나씩 꺼내서 옮긴다.
2. 후위 표기법으로 바뀐 수식을 계산하여 그 결과를 얻는다.

```python
def get_token_list(expr): # 연산을 쪼개서 리스트에 입력
    temp = []
    result = []
    num = str()

    for i in expr:
        if i == "+" or i =="-" or i == "*" or i == "/" or i == "(" or i == ")":
            for j in temp:
                num = num + j
            if num != "": # 공백 들어가는 것 방지
                result.append(float(num))
            result.append(j)
            temp = []
            num = ""
        else: # 두자리 이상 숫자는 문자열 덧셈으로 처리
            temp.append(i)
    for k in temp:
        num += k
    result.append(float(num))
    return result

def infix_to_postfix(prob, opStack, outStack):
    for i in prob:
        if i == "*" or i == "/" or i == "(": # 우선순위가 높은 연산자는 그냥 들어감
            opStack.push(i)
        elif i == "+" or i =="-":
            if opStack.len_stack() == 0: #opStack에 하나도 없으면 그냥 추가함
                opStack.push(i)
            else:
                for j in range(opStack.len_stack()): # 우선순위가 낮은 게 들어오면 높은 연산자를 opStack에 빼버림
                    if opStack.top() == "*" or opStack.top() == "/":
                        outStack.append(opStack.top())
                        opStack.pop()
                    opStack.push(i)
        elif i == ")": # 여는 괄호가 나올 때까지 ㅔㅐㅔ
            while (opStack.top() != "("):
                outStack.append(opStack.top())
                opStack.pop()
            opStack.pop()
        else: # 연산자가 아닌 경우 outStack에 추가
            outStack.append(i)
    while (opStack.len_stack() != 0):
        outStack.append(opStack.top())
        opStack.pop()

def compute_postfix(outStack):
    temp = Stack()

    for i in outStack:
        if i != "+" or i != "-" or i!= "*" or i != "/": # 연산자가 아니면 temp에 넣음
            temp.push(i)
        else:
            operand1 = temp.top()
            temp.pop()
            operand2 = temp.top()
            temp.pop()
            if (i == "+"):
                temp.push(operand2+operand1)
            elif (i == "-"):
                temp.push(operand2-operand1)
            elif (i == "+"):
                temp.push(operand2*operand1)
            elif (i == "+"):
                temp.push(operand2/operand1)
    return temp.pop()
```

<br>
