---
layout: post
title: Ch 12. 정렬 2
subtitle: 윤성우의 열혈 자료구조
cover-img: /assets/img/black.jpg
thumbnail-img: https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4ad0d30f-c2e9-4bac-a1a1-a2277a672fae/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T195114Z&X-Amz-Expires=86400&X-Amz-Signature=19a8338fcc03e75a3a0c00fb8d61dd1b6b3832c4e2e16d2c9a5af6091fd0f5d8&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject
share-img: /assets/img/path.jpg
tags: [자료구조]
---

# 12-1 균형 잡힌 이진 탐색 트리: AVL 트리의 이해

## 이진 탐색 트리의 문제점

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4ad0d30f-c2e9-4bac-a1a1-a2277a672fae/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T195114Z&X-Amz-Expires=86400&X-Amz-Signature=19a8338fcc03e75a3a0c00fb8d61dd1b6b3832c4e2e16d2c9a5af6091fd0f5d8&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/cad386d1-62d4-41f9-9db6-1b9b2e701bbb/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T195128Z&X-Amz-Expires=86400&X-Amz-Signature=10f650277a9353a5d70b75c9dbf34057f717c217580dd302ba70ee59e1b87b7b&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

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
            
            ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b1dfa232-3572-4c0c-9e62-3de948ebe265/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T195313Z&X-Amz-Expires=86400&X-Amz-Signature=057926430acf36b0bc6b505693047468d234ccee45cfef1bd634d2a0656f7dcc&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
     
<br>

## 리밸런싱이 필요한 상태 4가지

- LL 회전
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/433266b3-940b-4607-b87e-b36fd1d30b58/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T195346Z&X-Amz-Expires=86400&X-Amz-Signature=9766df21538d17c8f1dfaa0f5a53adc31fa2098bf0b52dd1748336bf93451781&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/fb3e58d5-1aa3-4cfe-acec-77e88686210a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T195358Z&X-Amz-Expires=86400&X-Amz-Signature=1dd1521ed75f73bcf799225f0759d0fea5e81054bcd0de0fa45e8f8b5a7574fc&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    균형 인수 +2가 연출된 상태  
    LL 회전은 왼쪽으로 두번 돌린다는 뜻이 아니고, LL상태에서 균형을 잡기 위해 필요한 회전이라는 의미이다.  
    
- RR 회전
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e77dbeef-6c8d-4487-841b-0f5572c17b13/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T195421Z&X-Amz-Expires=86400&X-Amz-Signature=9ec09b93c492ed926d4906fcc6979d1a5844904231c3279955431942a44849fd&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    RR 회전은 RR 상태의 이진 탐색 트리를 회전시키는 것
    
- LR 회전
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/33f8c4a1-3e75-4072-875e-3f3dcb4fe9c9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T195438Z&X-Amz-Expires=86400&X-Amz-Signature=856f96314dff421dedb0484e1cab8bf14fefad2f798c4b526177897104e54444&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    LR 상태는 한 번의 회전으로는 균형을 잡을 수 없기 때문에 LL, RR 상태보다 균형을 잡기 까다로움
    
    1. RR 회전의 부수적인 효과를 이용하여 LR 상태를 LL 상태로 바꾼다
        1. RR 회전의 부수적인 효과
            1. 부모 노드와 자식 노드의 관계가 바뀐다.
            2. 오른쪽으로 형성되었던 부모와 자식의 관계가 왼쪽으로 바뀐다.
    2. 이후 LL 회전을 시키면 리밸런싱이 완료된다
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4284d44a-13f9-4a93-9760-dfadf2d07dd9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T195503Z&X-Amz-Expires=86400&X-Amz-Signature=51f4e2130933d45d18d0b0a170e818de0e81f5a4889dd3e47c7de7eb29667cf7&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
- RL 회전
    
    부분적 LL 회전 → RR 회전
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0a6c6cd6-80ed-48d9-b053-7e46e7628f99/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T195558Z&X-Amz-Expires=86400&X-Amz-Signature=ccf7bc2a584c80d685a7fdbf82422d61235e49f2300b72fdd9fe2ee80e900c6c&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

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