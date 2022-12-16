---
layout: post
title: Ch 12. 탐색 2
subtitle: 윤성우의 열혈 자료구조
cover-img: /assets/img/black.jpg
thumbnail-img: https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fy3XVT%2FbtrSJxrfNOO%2FK5aW8PMqmK1EcZ4LIk8Y4K%2Fimg.png
share-img: /assets/img/path.jpg
tags: [자료구조]
---

# 12-1 균형 잡힌 이진 탐색 트리: AVL 트리의 이해

## 이진 탐색 트리의 문제점

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fy3XVT%2FbtrSJxrfNOO%2FK5aW8PMqmK1EcZ4LIk8Y4K%2Fimg.png)

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FAwHN1%2FbtrSIP6Zbgt%2FjhdDfFe0En5usBEK9uBLn0%2Fimg.png)

저장 순서만 바꿔도 어느 정도 균형이 잡히고 트리의 높이가 반으로 줄어듦

<aside>
💡 이진 탐색 트리는 저장 순서에 따라 탐색의 성능에 큰 차이가 있다
</aside>
<br>
- 균형 잡힌 이진 트리
    - AVL 트리
    - 2-3 트리
    - 2-3-4 트리
    - Red-Black 트리
    - B 트리

<br>

## AVL 트리와 균형 인수

- AVL 트리
    - 노드가 추가, 삭제될 때 트리의 균형 상태를 파악해서 스스로 구조를 변경하여 균형을 잡는 트리
    - 균형 인수의 절댓값이 2 이상인 경우 트리의 재조정 진행
    - 균형 인수: 균형의 정도를 표현하기 위한 것
        - `균형 인수 = 왼쪽 서브 트리의 높이 - 오른쪽 서브 트리의 높이`
            
            ![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb8ZAH9%2FbtrSJTHBsH0%2FPAYHMMJeX81U1pzXpdCxAK%2Fimg.png)
     
<br>

## 리밸런싱이 필요한 상태 4가지

- LL 회전
    
    ![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbhnJUr%2FbtrSM3P97hO%2FpmpRCCOuojaqmW7gLvq19K%2Fimg.png)
    
    ![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdaGkqr%2FbtrSITnYKXZ%2FRQFhV4KwDj9Xa7frhpypuK%2Fimg.png)
    
    균형 인수 +2가 연출된 상태  
    LL 회전은 왼쪽으로 두번 돌린다는 뜻이 아니고, LL상태에서 균형을 잡기 위해 필요한 회전이라는 의미이다.  
    
- RR 회전
    
    ![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FTR2jM%2FbtrSL07dxQe%2Fcqp9IyUr0kIC0yGITXitO0%2Fimg.png)
    
    RR 회전은 RR 상태의 이진 탐색 트리를 회전시키는 것
    
- LR 회전
    
    LR 상태는 한 번의 회전으로는 균형을 잡을 수 없기 때문에 LL, RR 상태보다 균형을 잡기 까다로움
    
    1. RR 회전의 부수적인 효과를 이용하여 LR 상태를 LL 상태로 바꾼다
        1. RR 회전의 부수적인 효과
            1. 부모 노드와 자식 노드의 관계가 바뀐다.
            2. 오른쪽으로 형성되었던 부모와 자식의 관계가 왼쪽으로 바뀐다.
    2. 이후 LL 회전을 시키면 리밸런싱이 완료된다
    
    ![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FmFvxP%2FbtrSJxdJGYy%2FwBiX959ZjJXrMoUjwdtv6K%2Fimg.png)
    
- RL 회전
    
    부분적 LL 회전 → RR 회전
    
    ![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FqJjRZ%2FbtrSMI6pXVo%2FzzD1BUlfRvJHxQFOESYwY1%2Fimg.png)

<br>

---

# 12-2 균형 잡힌 이진 탐색 트리: AVL 트리의 구현

```python
class Node:
    def __init__(self, key, height, left=None, right=None): # 초기화
        self.key = key
        self.height = height
        self.left = left
        self.right = right

class AVL:
    def __init__(self):
        self.root = None

    def height(self, n):
        if n == None:
            return 0
        return n.height

    def put(self, key):
        self.root = self.put_item(self.root, key)
	
    # 노드 추가
    def put_item(self, n, key):
        if n == None:
            return  Node(key, 1)
        if n.key > key:
            n.left = self.put_item(n.left, key)
        elif n.key < key:
            n.right = self.put_item(n.right, key)
        n.height = max(self.height(n.left), self.height(n.right))+1
        return self.balance(n)

    def balance(self, n):
        if self.bf(n) > 1: # 왼쪽 서브트리 불균형
            if self.bf(n.left) < 0: # 노드 n의 왼쪽 자식의 오른쪽 서브트리가 높은 경우
                n.left = self.rotate_left(n.left) # LR 회전
            n = self.rotate_right(n) # LL 회전

        elif self.bf(n) < -1: # 오른쪽 서브트리 불균형
            if self.bf(n.right) > 0: # 노드 n의 오른쪽 자식의 왼쪽 서브트리가 높은 경우
                n.right = self.rotate_right(n.right) #RL 회전
            n = self.rotate_left(n) #RR 회전
        return n

	# 균형 인수
    def bf(self, n):
        return self.height(n.left)-self.height(n.right)

    def rotate_right(self, n): #오른쪽 회전
        x = n.left
        n.left = x.right
        x.right = n
        n.height = max(self.height(n.left), self.height(n.right)) + 1
        x.height = max(self.height(x.left), self.height(x.right)) + 1
        return x

    def rotate_left(self, n): #왼쪽 회전
        x = n.right
        n.right = x.left
        x.left = n
        n.height = max(self.height(n.left), self.height(n.right)) + 1
        x.height = max(self.height(x.left), self.height(x.right)) + 1
        return x

    def preorder(self, n):
        print(str(n.key),' ', end="")
        if n.left:
            self.preorder(n.left)
        if n.right:
            self.preorder(n.right)

    def inorder(self, n):
        if n.left:
            self.inorder(n.left)
        print(str(n.key), ' ', end="")
        if n.right:
            self.inorder(n.right)

if __name__=="__main__":
    aa = AVL()
    aa.put(10)
    aa.put(20)
    aa.put(30)
    aa.put(40)
    aa.put(50)
    aa.put(29)
    aa.inorder(aa.root)
```

**오른쪽 회전의 알고리즘**

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcn4hn7%2FbtrSIo2RerN%2FQPJF9WJmnZAyIplgOXpdZ0%2Fimg.png)

루트 노드 n에서 불균형이 발견된다면, n.left를 x로 선언한다.  
n.left를 x.right로 만들어줘 연결을 끊는다.  
x.right에 n을 연결해줘 서브트리로 갱신한다.   
왼쪽 회전은 방향만 바꿔주면 된다.  

<br>
화일처리 과목 배울 때 AVL 트리를 배우긴 했는데 구현은 처음 해보네요.  
트리를 회전한다는 개념이 재밌는 것 같습니다 ㅎㅎ  
  
다음 글은 Ch 14. 그래프입니다!  
Ch 13. 테이블과 해쉬은 이해를 완벽히 못 해서 ㅠㅠ 천천히 올려보겠습니다.  

<br>