---
layout: post
title: Ch 9. 우선순위 큐와 힙
subtitle: 윤성우의 열혈 자료구조
cover-img: /assets/img/black.jpg
thumbnail-img: https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbmZfgG%2FbtrSqYvShOO%2F6ht8EoIYA0sfl6s0lo8Sok%2Fimg.png
share-img: /assets/img/path.jpg
tags: [자료구조]
---

# 09-1 우선순위 큐의 이해

## 우선순위 큐

들어간 순서에 상관없이 우선순위가 높은 데이터가 먼저 나온다.

- enqueue 우선순위 큐에 데이터를 삽입하는 행위
- dequeue 우선순위 큐에서 데이터를 꺼내는 행위

<br>

## 우선순위 큐의 구현 방법

1. 배열 기반 구현  
    데이터 삽입, 삭제 시 데이터를 한 칸씩 이동하는 연산을 수반한다  
    삽입의 위치를 찾기 위해 배열에 저장된 모든 데이터와 우선순위 비교를 해야 할 수도 있다  
    
2. 연결 리스트 기반 구현  
    삽입의 위치를 찾기 위해 배열에 저장된 모든 데이터와 우선순위 비교를 해야 할 수도 있다  
    
3. 힙 이용

<br>

## 힙(Heap)의 소개

이진 트리이되 완전 이진 트리  
모든 노드에 저장된 값은 자신 노드에 저장된 값보다 크거나 같아야 한다.  

![heap](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbmZfgG%2FbtrSqYvShOO%2F6ht8EoIYA0sfl6s0lo8Sok%2Fimg.png)

<br>

---

# 09-2 힙의 구현과 우선순위 큐의 완성

## 힙에서의 데이터 저장 과정(최소 힙 기준)

1. 새로운 데이터는 우선순위가 가장 낮다는 가정 하에 ‘마지막 위치’에 저장
2. 부모 노드와 우선순위를 비교하여 위치가 바뀌어야 한다면 바꿔준다  
    <aside>
    💡 자식 노드의 데이터 우선순위 ≤ 부모 노드 데이터의 우선순위
    </aside>
    
3. 제대로 된 위치를 찾을 때까지 계속해서 부모 노드와 비교

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbrrGRg%2FbtrSq9RDEnw%2FQXXqQ4ZZXBG8shRy6NHRkK%2Fimg.png)

<br>

## 힙에서의 데이터 삭제 과정

1. 루트 노드를 삭제
2. 마지막 노드를 루트 노드의 자리로 옮긴 후, 자식 노드와 비교를 통해 제자리를 찾아가게 함

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbfLtGo%2FbtrStRCrdeE%2FCkINx01o7NylHnKlTdm9J0%2Fimg.png)

<br>

## 성능 평가

1. 배열 기반  
    데이터 저장의 시간 복잡도 **O(n)**  
    데이터 삭제의 시간 복잡도 **O(1)**  
    
2. 연결 리스트 기반  
    데이터 저장의 시간 복잡도 **O(n)**  
    데이터 삭제의 시간 복잡도 **O(1)**  
    
3. 힙 기반  
    트리의 높이에 해당하는 수만큼만 비교연산을 진행하면 된다  
    데이터 저장의 시간 복잡도 **O(log2n)**  
    데이터 삭제의 시간 복잡도 **O(log2n)**  

<br>

## 배열 기반 힙

<aside>
💡 왼쪽, 오른쪽 자식 노드의 인덱스 값을 얻는 방법, 부모 노드의 인덱스 값을 얻는 방법

</aside>

- 왼쪽 자식 노드의 인덱스 값   
    부모 노드의 인덱스 값 * 2  

- 오른쪽 자식 노드의 인덱스 값   
   부모 노드의 인덱스 값 * 2 + 1  

- 부모 노드의 인덱스 값   
    자식 노드의 인덱스 값 / 2  

**heapq 사용 x**
    
```python
import sys
input = sys.stdin.readline

heap = [float('inf')] # 배열의 빈 부분을 0 대신 무한으로 채워넣는다
capacity = 0 # 배열 용량

def push(heap, n):
    global capacity
    # heap의 자리가 부족할 경우 배열을 2배로 늘려나간다
    if len(heap)-1 == capacity:
        heap = heap + [float('inf')]*len(heap)
    
    capacity += 1
    heap[capacity] = n
    
    # above heapify
    tn = capacity
    while(tn > 1):
        if heap[tn] < heap[tn//2]:
            temp = heap[tn]
            heap[tn] = heap[tn//2]
            heap[tn//2] = temp
            tn//=2
        else:
            break
    return heap

def pop(heap):
    global capacity
    if capacity == 0: # heap이 비어 있으면
        return 0
    p = heap[1]
    heap[1] = heap[capacity]
    heap[capacity] = float('inf')
    
    # below heapify
    tn = 1
    while(capacity > tn*2):
        if heap[tn*2] == float('inf') and heap[tn*2+1] == float('inf'):
            break
            
        if heap[tn] > min(heap[tn*2], heap[tn*2+1]): # 부모노드가 자식 노드보다 크면
            temp = heap[tn]
            if heap[tn*2] < heap[tn*2+1]: # 왼쪽 자식노드가 작으면
                heap[tn] = heap[tn*2]
                heap[tn*2] = temp
                tn *= 2
            else: # 오른쪽 자식노드가 작으면
                heap[tn] = heap[tn*2+1]
                heap[tn*2+1] = temp
                tn = tn*2+1
        else:
            break
    capacity -= 1
    return p
    

for i in range(int(input())):
    x = int(input())
    if x:
        heap = push(heap,x)
    else:
        print(pop(heap))
```
    
**heapq 사용**
```python
import sys
import heapq
input = sys.stdin.readline

def heapsort(iterable):
	h = []
	result = []
	# 모든 원소를 차례대로 힙에 삽입
	for value in iterable:
		heapq.heappush(h, value)
	
	# 힙에 삽입된 모든 원소를 차례대로 꺼냄
	for i in range(len(h)):
		result.append(heapq.heappop(h))
	return result

n = int(input())
arr = []

for i in range(n):
	arr.append(int(input))

h = heapsort(arr)

for i in range(n):
	print(h[i], end=' ')
```

<br>
