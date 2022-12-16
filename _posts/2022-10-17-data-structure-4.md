---
layout: post
title: Ch 4. 연결 리스트 2
subtitle: 윤성우의 열혈 자료구조
cover-img: /assets/img/black.jpg
thumbnail-img: https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbrMdvl%2Fbtru9PPMAsS%2FXe0TnnQshSDk0COX2vxaI1%2Fimg.png
share-img: /assets/img/path.jpg
tags: [자료구조]
---

# 04-1 연결 리스트의 개념적인 이해

## 연결 리스트

연결 기반의 리스트

배열은 메모리의 특성이 정적이어서 메모리의 길이를 변경하는 것이 불가능하다.  
`연결 리스트는 메모리의 동적 할당 가능하다.`   

malloc 함수와 free 함수를 통해 메모리 동적 할당을 하는 C 언어와는 달리 파이썬은 메모리의 할당과 해제가 파이썬 인터프리터에 의해 자동으로 관리된다.

특정 데이터를 찾기 위한 순차 탐색에 있어 탐색 속도가 배열에 비해 느리다.

- 노드
    - 필요할 때마다 바구니를 하나씩 마련해서 그곳에 데이터를 저장하고 이들을 배열처럼 서로 연결
    - ‘데이터를 저장할 장소’와 ‘다른 변수를 가리키기 위한 장소’가 구분되어 있다

```python
# 노드 객체
class Node:
    def __init__(self, item):
        self.data = item
        self.next = None

# 연결 리스트 객체
class LinkedList:
    def __init__(self):
        self.head = Node('head')
        
    def find(self, item):
        cur_node = self.head
        while cur_node.data != item:
            cur_node = cur_node.next
        return cur_node
    
    def insert(self, pos, newNode):
        new_node = Node(newNode)
        cur_node = self.find(pos)
        new_node.next = cur_node.next
        cur_node.next = new_node

    def show(self):
        cur_node = self.head
        while cur_node.next is not None:
            print(cur_node.data, end=' -> ')
            cur_node = cur_node.next
        print(cur_node.data)

    def find_previous(self, item):
        cur_node = self.head
        while (cur_node.next is not None) and (cur_node.next.data != item):
            cur_node = cur_node.next
        return cur_node

    def remove(self, item):
        prev_node = self.find_previous(item)
        if prev_node.next is not None:
            prev_node.next = prev_node.next.next
        
a = LinkedList()
a.insert('head', '1')
a.insert('1', '2')
a.insert('2', '3')
a.insert('3', '4')
a.show()

a.remove('2')
a.remove('4')
a.show()
```

![실행결과](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbrMdvl%2Fbtru9PPMAsS%2FXe0TnnQshSDk0COX2vxaI1%2Fimg.png)

<br>

---

# 04-2 단순 연결 리스트의 ADT와 구현
## 정렬 기능이 추가된 연결 리스트의 ADT

```python
def __Init__(self): # 초기화
def getAt(self, pos): # 특정 값이 어디에 있는지 찾음
def insert(self, pos, newNode): # pos 위치에 값 삽입
def popAt(self, pos): # pos 위치의 값 반환 후 삭제
def sortList(self, head: Node)->Node: # 정렬
```

💡 새 노드를 추가할 때, 리스트의 머리와 꼬리 중 어디에 저장할 것인가

### 머리에 추가할 경우
장점 → 변수 tail 불필요  
단점 → 저장된 순서를 유지하지 않는다.  

### 꼬리에 추가할 경우
장점→ 저장된 순서가 유지된다.  
단점 → 변수 tail 필요  
`tail의 관리를 생략하기 위해 머리에 추가`  

<br>

## 더미 노드 기반 연결 리스트

![더미노드 기반 연결리스트](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbCfbwR%2FbtrvdwaAXOx%2FKDkFEKCjEgmfOKqG5TBm2k%2Fimg.png)

유효한 데이터를 지니지 않는 그냥 빈 노드  
리스트 맨 앞에 위치하므로, head가 항상 더미 노드를 가리키고 있다.  
더미 노드에 데이터는 저장되어 있지 않다.  

**더미 노드가 없는 경우,** 리스트가 비어 있으면 head.next와 같은 참조가 불가능하므로 리스트가 비어 있는 경우와 그렇지 않은 경우로 나누어 연산을 구현해야 한다.

**더미 노드를 추가한다면,** NULL 값을 가질지언정 항상 head.next의 참조가 가능하므로 경우를 나누지 않고 일관되게 연산을 구현할 수 있다

<br>

---

# 04-3 연결 리스트의 정렬 삽입의 구현

```python
def sortList_(head: Node)->Node:
    p = head
    lst: list= []
		while p:
        lst.append(p.data)
        p = p.next
		
		lst.sort()
		
		p = head
		for i in range(len(lst)):
        p.data = lst[i]
        p = p.next
		return head
```

- lst에 연결 리스트의 요소들을 넣고 내장함수 `sort()` 를 이용해 정렬해준다
- `p = head` 로 연결 리스트를 초기화한 다음, 리스트에 저장된 요소들을 연결 리스트로 이어준다.

<br>
