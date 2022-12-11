---
layout: post
title: Ch 5. 연결 리스트 3
subtitle: 윤성우의 열혈 자료구조
cover-img: /assets/img/black.jpg
thumbnail-img: https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8d7b512e-85b0-4901-8752-7dae1510c3e3/KakaoTalk_20220215_184828359.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T165330Z&X-Amz-Expires=86400&X-Amz-Signature=f364474de46b19e69a557d3c07027d3e63565c5bbc11b41d59f86af6c737f458&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22KakaoTalk_20220215_184828359.jpg%22&x-id=GetObject
share-img: /assets/img/path.jpg
tags: [자료구조]
---

# 05-1 원형 연결 리스트

## 원형 연결 리스트

마지막 노드가 첫 번째 노드를 가리켜서 연결의 형태가 원을 이루는 구조의 연결 리스트

![원형 연결 리스트](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8d7b512e-85b0-4901-8752-7dae1510c3e3/KakaoTalk_20220215_184828359.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T165330Z&X-Amz-Expires=86400&X-Amz-Signature=f364474de46b19e69a557d3c07027d3e63565c5bbc11b41d59f86af6c737f458&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22KakaoTalk_20220215_184828359.jpg%22&x-id=GetObject)

노드를 리스트의 머리에 추가하든지 꼬리에 추가하든지 비슷하다.  
포인터 변수 head가 무엇을 가리키는지의 차이만 있다. 

<br>

## 변형된 원형 연결 리스트

하나의 포인터 변수가 꼬리를 가리키게 한 원형 연결 리스트  
꼬리를 가리키는 포인터 변수 하나만 있어도 머리 또는 꼬리에 노드를 간단히 추가할 수 있다.  

꼬리를 가리키는 변수 👉 tail  
머리를 가리키는 변수 👉 tail.next  

```python
class CList:
    class Node:
        def __init__(self, item, link):
            self.item = item
            self.next = link

    def __init__(self):
        self.tail = None
        self.nodeCount = 0

    def is_empty(self):
        return self.nodeCount == 0

    def insert(self, item):
        new = self.Node(item, None)
        if self.is_empty(): # 연결리스트가 비어 있는 경우
            new.next = new
            self.tail = new
        else:
            new.next = self.tail.next
            self.tail.next = new
        self.nodeCount += 1

    def delete(self):
        if self.is_empty():
            print('Underflow')
        x = self.tail.next
        if self.nodeCount == 1: # 연결리스트에 노드가 1개인 경우
            self.tail = None
        else:
            self.tail.next = x.next
        self.nodeCount -= 1
        return x.item

    def show(self):
        if self.is_empty():
            print('리스트 비어 있음')
        else:
            first = self.tail.next
            p = first
            while p.next != first: # 첫 노드를 다시 방문하면 루프 중단
                print(p.item, '-> ', end='')
                p = p.next
            print(p.item)

c = CList()
c.insert('1')
c.insert('2')
c.insert('3')
c.insert('5')
c.show()

c.delete()
c.show()
```

![실행 결과](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d50ac840-03ae-4087-abb1-3210f6b4ae46/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T165432Z&X-Amz-Expires=86400&X-Amz-Signature=16d41fcc23cca8994b59d5d3d49dd4991fe50858725bbae55deec2127f465065&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

<br>

---

# 05-2 양방향 연결 리스트

## 양방향 연결 리스트

하나의 노드가 자신의 왼쪽과 오른쪽 노드를 동시에 가리키는 구조

![양방향 연결 리스트](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/21455ae3-4163-4dd8-9f16-412e16166d4c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T165514Z&X-Amz-Expires=86400&X-Amz-Signature=c2a2cb15db278a5d3fbd18a137ec9a31399f354f5bb8e76f9fab51450d504ab1&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- 장점    
    이전 노드의 주소를 알고 있으므로 마지막 노드를 삭제하는 경우 그 전 노드(previous)를 알기 위해 처음부터 탐색할 필요 없이 바로 삭제할 수 있다.

- 단점    
    링크를 한 개 더 가지므로 복잡하다.

```python
class Node:
    def __init__(self, item):
        self.item = item
        self.next = None
        self.previous = None

class DList:
    def __init__(self):
        self.head = Node('head')

    def find(self, item):
        curNode = self.head
        while curNode.item != item:
            curNode = curNode.next
        return curNode

    def insert(self, item, new):
        newNode = Node(new)
        curNode = self.find(item)
        newNode.next = curNode.next
        curNode.next = newNode
        newNode.previous = curNode

    def remove(self, item):
        curNode = self.find(item)
        curNode.previous.next = curNode.next
        curNode.previous = None
        if curNode.next is not None: # 삭제하려는 노드의 다음에 연결된 노드가 있으면
            curNode.next.previous = curNode.previous
            curNode.next = None

    def show(self):
        curNode = self.head
        while curNode.next is not None:
            print(curNode.item, end=' -> ')
            curNode = curNode.next
        print(curNode.item)

    def findLast(self):
        curNode = self.head
        while curNode.next is not None:
            curNode = curNode.next
        return curNode

    def showReverse(self):
        curNode = self.findLast()
        while curNode.previous is not None:
            print(curNode.item, end=' -> ')
            curNode = curNode.previous
        print(curNode.item)

d = DList()
d.insert('head', '1')
d.insert('1', '2')
d.insert('2', '3')
d.insert('3', '4')
d.show()

d.remove('4')
d.show()

d.showReverse()
```
![실행 결과](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ea189b57-261a-4389-b85d-7fdbed8431ac/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T165823Z&X-Amz-Expires=86400&X-Amz-Signature=d97b075bce44da7599405a66c3c48d97391a133e28c63468e7511449713046ca&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

<br>
