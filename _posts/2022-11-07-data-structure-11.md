---
layout: post
title: Ch 11. 정렬 1
subtitle: 윤성우의 열혈 자료구조
cover-img: /assets/img/black.jpg
thumbnail-img: https://s3.us-west-2.amazonaws.com/secure.notion-static.com/37dfe85d-986b-464b-889b-13f9b7dcb705/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T194243Z&X-Amz-Expires=86400&X-Amz-Signature=e9a90c16a2facb4b8b5948e82ab047719e754ce6f3af05481ccb50e6231be284&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject
share-img: /assets/img/path.jpg
tags: [자료구조]
---

# 11-1 탐색의 이해와 보간 탐색

## 보간 탐색

이진 탐색의 비효율성을 개선한 알고리즘  
탐색대상이 앞쪽에 위치해 있으면 앞쪽에서 탐색을 시작하여 개선  
예) 전화번호부에서 ‘김정수’라는 사람의 전화번호를 찾을 때 ‘ㄱ’에 해당하는 앞쪽에서 찾음  

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/37dfe85d-986b-464b-889b-13f9b7dcb705/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T194243Z&X-Amz-Expires=86400&X-Amz-Signature=e9a90c16a2facb4b8b5948e82ab047719e754ce6f3af05481ccb50e6231be284&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

*A:Q=high - low : s - low*

*s= Q/A(high - low)+low*

*s=(x-arr[low])/(arr[high]-arr[low])*(high-low)+low*

- 단점  
    오차율을 최소화하기 위해 정수형 나눗셈이 아닌 실수형 나눗셈을 진행

<br>

## 보간탐색 구현

```python
def interpolationSearch(arr, n, x):
	low = 0
	high = n-1
	s = 0
	while (arr[low] != arr[high] and x >= arr[low] and x <= arr[high]):
    s = low + (float((high - low) / (arr[high] - arr[low])) * (x - arr[low]))
    if arr[s] == x:
      return s;
    elif arr[s] > x:
      high = s - 1
    else:
      low = s + 1

  if (x == arr[low]):
    return low
  else:
    return -1
```

- 탈출조건  
    ```python
    while ( ... x ≥ arr[low] and x≤ arr[high]):  
        ...  
        return -1
    ```

<br>  

---

# 11-2 이진 탐색 트리

## 이진 탐색 트리

이진트리 + 데이터 저장 규칙

- 규칙
    - 이진 탐색 트리의 노드에 저장된 키는 유일하다
    - 루트 노드의 키가 왼쪽 서브 트리를 구성하는 어떠한 노드의 키보다 크다
    - 루트 노드의 키가 오른쪽 서브 트리를 구성하는 어떠한 노드의 키보다 작다
    - 왼쪽과 오른쪽 서브 트리도 이진 탐색 트리이다

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6643d46d-5b46-4b47-b899-c313ab471bb1/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T194524Z&X-Amz-Expires=86400&X-Amz-Signature=7fede0d8c62ad02d850463371be38c2dccb8075d3a35c720a8779284dcb730ca&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

<aside>
💡 왼쪽 자식 노드의 키 < 부모 노드의 키 < 오른쪽 자식 노드의 키
</aside>

<br>

## 이진 탐색 트리의 구현

- 삭제
    
    **case1**: 자식노드가 2개 있을 경우
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6f0bcd66-9899-47b2-a6ff-b4fa662fc2df/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T194558Z&X-Amz-Expires=86400&X-Amz-Signature=b1da2d5dd8852118d42afba3c9d7157b56d918ed0e638a2955716018f21224ef&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0e6ff322-ce41-43f6-bdac-f229e02913a5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T194612Z&X-Amz-Expires=86400&X-Amz-Signature=559295a9773864e45a9bcc80ec694af42db76815d47c96c0f0c41741d58c702d&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    **case2**: 자식노드가 1개 있을 경우
    
    **case3**: 자식노드가 없을 경우
    ```python
    class Node(object):
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

    class BinarySearchTree(object):
        def __init__(self):
            self.root = None

        # 삽입
        def insert(self, data):
            self.root = self._insert_value(self.root, data)
            return self.root is not None
    
        def _insert_value(self, node, data):
            if node is None:
                node = Node(data)
            else:
                if data <= node.data:
                    node.left = self._insert_value(node.left, data)
                else:
                    node.right = self._insert_value(node.right, data)
            return node
            
        # 탐색
        def find(self, key):
            return self._find_value(self.root, key)
    
        def _find_value(self, root, key):
            if root is None or root.data == key:
                return root is not None
            elif key < root.data:
                return self._find_value(root.left, key)
            else:
                return self._find_value(root.right, key)
        
        # 삭제
        def delete(self, key):
            self.root, deleted = self._delete_value(self.root, key)
            return deleted
    
        def _delete_value(self, node, key):
            if node is None:
                return node, False
    
            deleted = False
            if key == node.data:
                deleted = True
                if node.left and node.right: # 자식 노드가 2개인 경우
                    parent, child = node, node.right
                    # 오른쪽 서브트리에서 left로 이동하여 가장 작은 값을 찾음
                    while child.left is not None:
                        parent, child = child, child.left
                    # key 값의 left 자식 노드 값을 가장 작은 값의 왼쪽에 붙임
                    child.left = node.left

                    # 삭제하려는 노드의 오른쪽 노드가 가장 작은 값일 때 고려
                    if parent != node:
                        parent.left = child.right
                        child.right = node.right
                    node = child
                elif node.left or node.right: # 자식 노드가 1개인 경우
                    node = node.left or node.right # 자식 노드를 끌어다 놓음
                else: # 자식 노드가 없는 경우
                    node = None # 값 삭제
            elif key < node.data: # 키 값이 부모 노드보다 작다면 left 자식 노드로
                node.left, deleted = self._delete_value(node.left, key)
            else: # 키 값이 부모 노드보다 크다면 right 자식 노드로
                node.right, deleted = self._delete_value(node.right, key)
            return node, deleted


    array = [40, 4, 34, 45, 14, 55, 48, 13, 15, 49, 47]
    
    bst = BinarySearchTree()
    for x in array:
        bst.insert(x)
    
    # Find
    print(bst.find(15)) # True
    print(bst.find(17)) # False

    # Delete
    print(bst.delete(55)) # True
    print(bst.delete(14)) # True
    print(bst.delete(11)) # False
    ```

다음 글은 Ch 11. 탐색 2입니다!  
탐색을 마무리해보겠습니다 ..  

<br>
