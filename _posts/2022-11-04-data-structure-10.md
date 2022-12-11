---
layout: post
title: Ch 10. 정렬
subtitle: 윤성우의 열혈 자료구조
cover-img: /assets/img/black.jpg
thumbnail-img: https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f4985344-19bd-419e-b2be-d1ebe44a6fb4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T192856Z&X-Amz-Expires=86400&X-Amz-Signature=f969b2ec0474bcdbeee8feac2a285c5884a170166fb727e8968ae70d42fb9353&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject
share-img: /assets/img/path.jpg
tags: [자료구조]
---

# 10-1 단순한 정렬 알고리즘

## 버블 정렬

인접한 두 개의 데이터를 비교해가면서 정렬을 진행   
정렬순서 상 위치가 바뀌어야 하는 경우 두 데이터의 위치를 바꿔나감   

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f4985344-19bd-419e-b2be-d1ebe44a6fb4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T192856Z&X-Amz-Expires=86400&X-Amz-Signature=f969b2ec0474bcdbeee8feac2a285c5884a170166fb727e8968ae70d42fb9353&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

### 버블 정렬 구현
    
```python
def bubbleSort(arr): # 오름차순 정렬
    n = len(arr)
    for i in range(n-1, -1, -1):
        for j in range(0, i):
            if arr[j] > arr[j+1]: # 앞의 숫자가 작으면
                arr[j], arr[j+1] = arr[j+1], arr[j]
    return arr
```
    

### 성능 평가

- 비교 횟수 `O(n^2)`
    
    <aside>
    💡 if arr[j] > arr[j+1]:
    </aside>
    *(n-1) + (n-2) + ... + 2 + 1 = n(n-1)/2*
    
- 이동 횟수  
    - 최선의 경우  
        데이터가 이미 정렬되어 있는 상태라면 데이터의 이동이 일어나지 않는다.
    - 최악의 경우 `O(n^2)`  
        역순으로 정렬된 상태라면 비교의 횟수와 이동의 횟수가 같다.

<br>

## 선택 정렬

정렬순서에 맞게 하나씩 선택해서 옮기는, 옮기면서 정렬이 되게 하는 알고리즘  
별도의 메모리 공간 필요  

→ **개선된 선택 정렬**

정렬순서 상 가장 앞서는 것을 선택해 가장 왼쪽으로 이동시키고, 원래 그 자리에 있던 데이터는 빈 자리에 가져다 놓음

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9c9b826f-7f44-4422-91d8-081d3ef42885/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T193222Z&X-Amz-Expires=86400&X-Amz-Signature=8d9697201e05e86e4d94c899a8445faba324d29fe65823ace1bdecefb6b8a997&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

### 선택 정렬 구현
    
```python
def selectionSort(arr):
    n = len(arr)
    for i in range(n-1):
        indexMin = i
        for j in range(i+1, n):
            if arr[indexMin] > arr[j]: # 가장 작은 값을 갖고 있는 인덱스를 찾음
                indexMin = j
        arr[i], arr[indexMin] = arr[indexMin], arr[i] # 정렬이 안 된 부분 중에서 교환
    return arr
```
    

### 성능 평가

- 비교 횟수 `O(n^2)`  

    <aside>
    💡 if arr[indexMin] > arr[j]:
    </aside>
    
    *(n-1) + (n-2) + ... + 2 + 1 = n(n-1)/2*
    
- 이동 횟수 `O(n)`

<br>

## 삽입 정렬

정렬 대상을 두 부분으로 나눠서, 정렬 안 된 부분에 있는 데이터를 정렬된 부분의 특정 위치에 삽입해 가면서 정렬을 진행

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b3ff33fe-b7d8-4f85-b4eb-3bb8671947aa/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T193412Z&X-Amz-Expires=86400&X-Amz-Signature=d536d938275eca3cfea0947b2e7399f4236463cc342f5792680664a26a10e352&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

### 삽입 정렬 구현
    
```python
def insertionSort(arr):
    n = len(arr)
    for i in range(1, n):
        j = i - 1
        while (j >= 0 and arr[j] > arr[i]):
            arr[j+1] = arr[j] # 뒤로 한 칸씩 이동
            j = j - 1

        arr[j+1] = arr[i] # 삽입
    return arr
```
    

### 성능 평가

- 비교 횟수 `O(n^2)`
    
    *1+ 2 + ... + (n-2) + (n-1) = n(n-1)/2*
    
- 이동 횟수 `O(n^2)`
    
    <aside>
    💡 while (j >= 0 and arr[j] > arr[i]):
    	arr[j+1] = arr[j] # 데이터 이동의 핵심 연산
    
    </aside>
    
<br>

---

# 10-2 복잡하지만 효율적인 정렬 알고리즘

## 힙 정렬

힙의 루트 노드에 저장된 값이 정렬순서 상 가장 앞선다

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a4922723-621d-4fe7-b718-744cd5f040ce/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T193505Z&X-Amz-Expires=86400&X-Amz-Signature=2eae513e0deab4caf0e3ca0e6e1acb58124cf797519febbee37e191fd456cd3e&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

### 힙 정렬 구현
    
```python
def heapify(arr, idx, n):
    left = idx * 2;
    right= idx * 2 + 1;
    s_idx = idx
    if (left <= n and arr[s_idx] > arr[left]):
        s_idx = left
    if (right <= n and arr[s_idx] > arr[right]):
        s_idx = right
    if s_idx != idx:
        arr[idx], arr[s_idx] = arr[s_idx], arr[idx]
        return heapify(arr, s_idx, n) # 레벨이 내려감

def heapSort(v):
    n = len(v)
    v = [0] + n # 인덱스 1부터 시작
    # 최소 힙 생성, 오름차순
    for i in range(n, 0, -1):
        heapify(v, i, n)

    for i in range(n, 0, -1):
        print(v[1])
        v[i], v[1] = v[1], v[i] # 단말 노드가 루트 노드로
        heapify(v, 1, i-1) # 힙 구성
```
    

### 성능 평가

- 데이터 저장, 삭제 `O(log2n)`
    
    정렬대상의 수가 n개라면, `O(nlog2n)`
    
<br>

## 병합 정렬

분할 정복 기법에 근거하여 만들어짐

전체 데이터를 하나씩 구분이 될 때까지 분할한 후, 정렬순서를 고려하여 하나로 묶는다

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e1fb46d2-7340-4d2b-aad5-6370865b9226/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T193555Z&X-Amz-Expires=86400&X-Amz-Signature=3adb8bf2ad16a9b656edc7a088093d82bf15462f375d35f735d6e6fe1812c400&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

### 병합 정렬 구현
    
```python
def mergeSort(lst):
    if len(lst) <= 1:
        return lst
    mid = len(lst) // 2
    leftList = lst[:mid]
    rightList = lst[mid:]
    leftList = mergeSort(leftList)
    rightList = mergeSort(rightList)
    return merge(leftList, rightList)

def merge(left, right):
    result = []
    while (len(left) > 0 or len(right) > 0):
        if (len(left) > 0 and len(right) > 0): # 둘중 원소가 하나도 남지 않을 때까지
            if left[0] <= right[0]: # 작은 값을 result에 저장
                result.append(left[0])
                left = left[1:]
            else:
                result.append(right[0])
                right = right[1:]
        elif len(left) > 0:
            result.append(left[0])
            left = left[1:]
        elif len(right) > 0:
            result.append(right[0])
            right = right[1:]
    return result
```
    

### 성능 평가

정렬대상의 수가 n개일 때, 각 병합의 단계마다 최대 n번의 비교연산이 진행   
`O(nlog2n)`

<br>

## 퀵 정렬

분할 정복 기법에 근거하여 만들어짐

- 리스트 가운데서 하나의 원소, 피벗(pivot)을 고름
- 피벗 앞에는 피벗보다 작은 값, 뒤에는 큰 값이 오도록 하여 리스트를 둘로 분할
- 분할된 두 개 리스트 각각에 재귀적으로 이 과정을 반복

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/091690b0-1e1c-4857-a8b9-a2a34cccb060/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T193643Z&X-Amz-Expires=86400&X-Amz-Signature=46f6f0e9cf3cdc04837c839df0d67e7ee3f67377243da0e71ad2f15bb17b679e&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

### 퀵 정렬 구현
    
```python
def quickSort(arr):
    n = len(arr)
    if (n <= 1):
        return arr
    else:
        pivot = arr[0]
        greater = [ element for element in arr[1:] if element > pivot ]
        lesser = [ element for element in arr[1:] if element <= pivot ]
        return quickSort(lesser) + [pivot] + quickSort(greater)
```
    

### 성능 평가

- 최선의 경우 `O(nlog2n)`  
    하나의 피벗이 제자리를 찾아가는 과정에서 발생하는 비교연산의 횟수: n  
    분할은 log2n 단계를 거쳐 이뤄짐  
    
- 최악의 경우 `O(n^2)`  
    이미 데이터들이 정렬되어 있고 피벗이 가장 작은 값으로 결정되는 상황
    
<br>

## 기수 정렬

기수(데이터를 구성하는 기본 요소)를 이용하여 정렬을 진행  
적용할 수 있는 범위가 제한적  
기수 정렬의 예) 영단어 red, why, zoo를 사전편찬 순서대로 정렬  

### LSD vs MSD

**LSD**

덜 중요한 자릿수에서부터 정렬을 진행

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a1b6f480-7654-4818-a9ca-497fc704b9da/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T193746Z&X-Amz-Expires=86400&X-Amz-Signature=e29e3341886616f9f1e95982f8c554ac2b44460f2dd73df9307c751f0237ca37&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

**MSD**

가장 중요한 자릿수에서부터 정렬이 진행  
멈추지 않고 마지막 단계까지 진행했기 때문에 잘못된 결과 초래  
중간에 데이터를 점검해야 함  

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0b5ad650-f93b-485e-9e34-713061599051/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221211T193800Z&X-Amz-Expires=86400&X-Amz-Signature=4baf2180c0ac873667a8bba1b25896d722f20c8c0022c0a863a6b7f131a1babe&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

### 기수 정렬 구현(LSD)
    
```python
def radixSort(arr, base=10):
    n = len(arr)
    maxval = max(arr)
    exp = 1
    while exp <= maxval:
        output = [0] * n
        count = [0] * n
        for i in range(n):
                        count[(arr[i]//exp)%base] += 1
        for i in range(1, base):
                        count[i] += count[i-1]
        for i in range(size-1, -1, -1):
                j = (arr[i]//exp) % base
                output[count[j]-1] = arr[i]
                count[j] -= 1
        for i in range(size):
                        arr[i] = output[i]
        exp *= base
        return arr
```
    

### 성능 평가
모든 정렬대상의 길이가 l이라 할 때, `O(ln)`

<br>
저는 선택 정렬과 삽입 정렬이 항상 헷갈리더라구요..  

선택 정렬은 가장 작은 값을 골라서 첫 번째 요소(정렬이 안 된 부분에서)와 교환하는 방식이고,  
삽입 정렬은 주어진 순서대로 정렬을 진행하는데 요소의 알맞은 위치를 찾아서 넣는 방식으로 이해했습니다.


다음 글은 Ch 11. 탐색 1입니다!

<br>