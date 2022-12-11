---
layout: post
title: Ch 8. 트리
subtitle: 윤성우의 열혈 자료구조
cover-img: /assets/img/black.jpg
thumbnail-img: https://s3.us-west-2.amazonaws.com/secure.notion-static.com/18093168-fcea-4201-bb1b-7bc8dacbcc0d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T170704Z&X-Amz-Expires=86400&X-Amz-Signature=5116e4b06cbd19135ea341293dfc048209426b966959d6290dd2a9518839410a&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject
share-img: /assets/img/path.jpg
tags: [자료구조]
---

# 08-1 트리의 개요

## 트리

계층적 관계를 ‘표현’하는 자료구조  
예) 컴퓨터의 디렉터리 구조, 기업 및 정부의 조직도

![트리](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/18093168-fcea-4201-bb1b-7bc8dacbcc0d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T170704Z&X-Amz-Expires=86400&X-Amz-Signature=5116e4b06cbd19135ea341293dfc048209426b966959d6290dd2a9518839410a&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![의사 결정 트리](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e3d00582-bfac-4596-bcc2-aea2f2deec85/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T170723Z&X-Amz-Expires=86400&X-Amz-Signature=d4c9b53c13ddf61cd6a424cab19d94380e317c667b99ee02aa0ba10200683b06&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

<br>

## 트리 관련 용어

- 노드: 트리의 구성요소에 해당하는 A~I와 같은 요소
- 간선: 노드와 노드를 연결하는 연결 선
- 루트 노드: 트리 구조의 최상위에 존재하는 A와 같은 노드
- 단말 노드(leaf node): 아래로 또 다른 노드가 연결되어 있지 않은 D, F, H, I와 같은 노드
- 내부 노드(비단말 노드): 단말 노드를 제외한 모든 노드로 A, B, C, E, G와 같은 노드

- 노드 A는 노드 B, C의 부모 노드
- 노드 B, C는 노드 A의 자식 노드
- 노드 B, C는 부모 노드가 같으므로, 서로가 서로에게 형제 노드

<br>

## 이진 트리와 서브 트리

![서브 트리](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/46b94e57-0020-440c-8825-a582ab67d74b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T170926Z&X-Amz-Expires=86400&X-Amz-Signature=5c6723ae1d3a0daa32517994ffb64d119882e09520de51747738dc578d93e3de&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

서브 트리: 큰 트리에 속하는 작은 트리

### 이진 트리(재귀적)
`루트 노드를 중심으로 두 개의 서브 트리로 나뉘어진다.`   
`나뉘어진 두 서브 트리도 모두 이진 트리여야 한다.`

+노드가 위치할 수 있는 곳에 노드가 없다면, 공집합 노드가 존재하는 것으로 간주한다.

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/18093168-fcea-4201-bb1b-7bc8dacbcc0d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T170704Z&X-Amz-Expires=86400&X-Amz-Signature=5116e4b06cbd19135ea341293dfc048209426b966959d6290dd2a9518839410a&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5287b65a-3e16-4c87-a78a-8497d1e3fb80/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T171142Z&X-Amz-Expires=86400&X-Amz-Signature=69f26442375b1ffa159916223e243a9350e61ac1dd7dfacf6641caccdfecf29c&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

<br>

## 포화 이진 트리와 완전 이진 트리

### 포화 이진 트리

모든 레벨이 꽉 차 있다.

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/475ac5d7-77be-4913-a57e-f76971289d00/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T171219Z&X-Amz-Expires=86400&X-Amz-Signature=e00e9ed022cf1023fc314fd55dbfa7c3e6c482bfc3c035d7988acfd4519451f9&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

### 완전 이진 트리

노드와 위에서 아래로, 왼쪽에서 오른쪽의 순서대로 채워진 이진트리

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8091e0e7-f22e-42b7-9ae1-bc8a2dcd7037/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T171223Z&X-Amz-Expires=86400&X-Amz-Signature=b71fc94792139f29625c0957efae02a3267bf5f08a2781364957ecc407948651&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

<br>

---

# 08-2 이진 트리의 구현

배열과 연결 리스트를 이용하여 구현 가능  
배열 기반 이진 트리는 연결 리스트 기반 이진 트리에 비해 탐색이 용이하고 빠름  

## 이진 트리의 ADT

```python
def __init__(self): # 트리 초기화

def is_empty(self): # 트리가 비어 있으면 True(1), 그렇지 않으면 False(0) 반환

def treesize(self): # 노드 개수

def rootnode(self): # 루트 노드 반환

def parent(self,v): # 특정 노드의 부모 노드 반환

def children(self,v): # 특정 노드의 자식 노드 반환

def addNode(self,v,data,location): # 트리에 노드 추가
```

<br>

## 이진 트리의 구현

```python
class Node:
  def __init__(self,data,L=None,R=None,parent=None):
    self.data = data
    self.L = L
    self.R = R
    self.parent = parent

class tree:
  def __init__(self):
    self.root = None
    self.n=0

  def isEmpty(self):
    return self.root==None
  
  def treesize(self):
    print(self.n)
    return self.n
  
  def rootnode(self):
    return self.root.data
  
  def parent(self,v):
    if v == self.root:
      print("Root Node")
    else:
      return v.parent.data
  
  def children(self,v):
    return v.L.data,v.R.data

  def isInternal(self,v): # 내부노드인지
    if v.L != None or v.R != None:
      return True
    else: 
      return False
  
  def isExternal(self,v): # 단말노드인지
    if v.L == None and v.R == None:
      return True
    else:
      return False
  
  def isRoot(self,v):
    if self.root == v:
      return True
    else:
      return False
  
  def setElements(self,v,e):
    tmp = v.data
    v.data = e
    print(f"Succesly set element v.data : {tmp}=> {e}")
  
  def addNode(self,v,data,location):
    if location =='L':
      v.L = Node(data,None,None,v)
      self.n+=1
    elif location == 'root':
      self.root = Node('Root')
      self.n+=1
    else:
      v.R = Node(data,None,None,v)
      self.n+=1
```

<br>

---

# 08-3 이진 트리의 순회

- 전위 순회: 루트 노드를 먼저 방문
- 중위 순회: 루트 노드를 중간에 방문
- 후위 순회: 루트 노드를 마지막에 방문

## 순회의 재귀적 표현

- 중위 순회
    ```python
    def inorder(self, n):
    	if n != None:
    		if n.left:
    			self.inorder(n.left)
    		print(n.item, end='') # 노드 방문
    		if n.right:
    			self.inorder(n.right)
    ```  

- 전위 순회
    ```python
    def preorder(self, n):
    	if n != None:
    		print(n.item, end='') # 노드 방문
    		if n.left:
    			self.inorder(n.left)
    		if n.right:
    			self.inorder(n.right)
    ```  
- 후위 순회
    ```python
    def postorder(self, n):
    	if n != None:
    		if n.left:
    			self.inorder(n.left)
    		if n.right:
    			self.inorder(n.right)
    		print(n.item, end='') # 노드 방문
    ```

<br>    

---

# 08-4 수식 트리의 구현

## 수식 트리

이진 트리를 이용해서 수식을 표현해 놓은 것

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6a85820d-b888-43bc-a84f-07e7d59e60ee/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T171429Z&X-Amz-Expires=86400&X-Amz-Signature=c59ea01f80b4728921c11b014f616383a0a4817def457782ad52c0fc240fe3fb&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

루트 노드에 저장된 연산자의 연산을 하되, 두 개의 자식 노드에 저장된 두 피연산자를 대상으로 연산을 한다.  
`중위 표기법의 수식 → 후위 표기법의 수식 → 수식 트리`

- 수식 트리의 구성과정에서 피연산자는 무조건 스택으로 옮긴다
- 연산자를 만나면 스택에 쌓여있는 두 개의 피연산자를 꺼내어 자식 노드로 연결한다.
- 자식 노드를 연결해서 만들어진 트리는 다시 스택으로 옮긴다.

```python
import re

def postfix_convert(infix):
    stk = [] # 스택
    cal = []
    expression = re.sub('([\+\-\*\/\(\)])', '\g<1>', infix)
    print("Postfix: ", end="")

    for x in expression.split():
        if x == '(':
            stk.append(x)
        elif x == '+' or x == '-':
            if '+' in stk or '-' in stk or '*' in stk or '/' in stk:
                pop_stk = stk.pop()
                if pop_stk == '(':
                    stk.append(pop_stk)
                    stk.append(x)
                else:
                    stk.append(pop_stk)
                    print(stk.pop(), end=" ")
                    cal.append(pop_stk)
                    stk.append(x)
            else:
                stk.append(x)
        elif x == "*" or x == '/':
            if '*' in stk or '/' in stk:
                print(stk.pop(), end=" ")
                cal.append(stk.pop())
                stk.append(x)
            else:
                stk.append(x)
        elif x == ")":
            while stk:
                p = stk.pop()
                if p == "(":
                    continue
                else:
                    print(p, end=" ")
                    cal.append(p)
        else:
            print(x, end=" ")
            cal.append(x)
    while stk:
        pop_stk2 = stk.pop()
        print(pop_stk2, end=" ")
        cal.append(pop_stk2)
    return cal

class Node(object):
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None

def create_expression_tree(infix):
    postfix = postfix_convert(infix)
    print("\n")
    stack = []
    cal_stack = []
    operator_precedance = {'(', ')', '+', '-', '*', '/'}

    for char in postfix:
        if char not in operator_precedance:
            node = Node(char)
            stack.append(node)
            cal_stack.append(node)
        else:
            node = Node(char)
            right = stack.pop()
            left = stack.pop()
            node.right = right
            node.left = left
            stack.append(node)
            print(char, "-> [child:", node.left.value, ", silbling:", node.right.value, "]")
            print()
            cal_right = cal_stack.pop()
            cal_left = cal_stack.pop()
            # 사칙연산 계산
            if char == "+":
                cal = float(cal_left.value) +float(cal_right.value)
                cal_node = Node(cal)
                cal_stack.append(cal_node)
            elif char == "-":
                cal = float(cal_left.value) - float(cal_right.value)
                cal_node = Node(cal)
                cal_stack.append(cal_node)
            elif char == "*":
                cal = float(cal_left.value) * float(cal_right.value)
                cal_node = Node(cal)
                cal_stack.append(cal_node)
            elif char == "/":
                cal = float(cal_left.value) / float(cal_right.value)
                cal_node = Node(cal)
                cal_stack.append(cal_node)

    print("root --> [", stack.pop().value, "]")
    print("\n계산결과 :", cal_stack.pop().value)

create_expression_tree("((3*4)+(6-8))")
```

<br>
