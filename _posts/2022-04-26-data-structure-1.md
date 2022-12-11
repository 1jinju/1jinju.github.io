---
layout: post
title: Ch 1. 자료구조와 알고리즘의 이해
subtitle: 윤성우의 열혈 자료구조
cover-img: /assets/img/black.jpg
thumbnail-img: /assets/img/datastructure-crop.PNG
share-img: /assets/img/path.jpg
tags: [자료구조]
---

# 01-1 자료구조에 대한 기본적인 이해   
## 자료구조  

**자료구조**: 데이터를 표현하고 저장하는 방법  
### 자료구조의 분류
- 선형구조
    - 리스트: 같은 값이 한 번 이상 존재할 수 있는 일련의 값이 모여있는 추상적 자료형
    - 스택: 후입선출(Last In First Out, LIFO) 특성을 가지는 자료구조
    - 큐: 선입선출(First in First Out, FIFO) 특성을 가지는 자료구조
      
- 비선형구조
    - 트리: 그래프의 일종으로, 노드로 이루어진 자료구조
    - 그래프: 단순히 노드와 그 노드를 연결하는 간선을 하나로 모아 놓은 자료구조
      
- 파일구조
    - 순차파일
    - 색인파일
    - 직접파일
      
- 단순구조
    - 정수
    - 실수
    - 문자
    - 문자열
  
### 자료구조와 알고리즘  
- 알고리즘  
    - 표현 및 저장된 데이터를 대상으로 하는 문제의 해결 방법  
    - 자료구조가 결정되어야 그에 따른 효율적인 알고리즘 결정 가능    

<br>

---
# 01-2 알고리즘의 성능분석 방법  
## 시간복잡도와 공간복잡도   
- 공간복잡도: 메모리 사용량에 대한 분석결과
- 시간복잡도
    - 속도에 해당하는 알고리즘의 수행시간 분석결과
    - 처리해야 할 데이터의 수 n에 대한 연산횟수의 함수 T(n)을 구성
 
![Crepe](https://th.bing.com/th/id/R.92d17527c2e6fce22062cd56614ef8dc?rik=kY7dD4k8R2D8sw&riu=http%3a%2f%2fblogfiles.naver.net%2f20100311_267%2fsunbeatz_1268290202273aq23N_jpg%2f10_sunbeatz.jpg&ehk=P50%2faxbe3OzYJBTsVrDvj6t%2bIYIfdNss%2fVjYSQH8xl0%3d&risl=&pid=ImgRaw&r=0)

👉 데이터 수가 적은 경우 알고리즘 C 이용  
👉 데이터 수가 많은 경우 알고리즘 A 이용

<br>

## 순차탐색 알고리즘의 시간복잡도   
```C
for (i = 0; i < len; i++) { 
	if (ar[i] == target)
		return i;
}
```  
탐색 알고리즘에서의 핵심은 동등비교를 하는 비교연산에 있다.  

 

### 최선의 경우   
    찾고자하는 값이 맨 앞에 있는 경우   

 

### 최악의 경우    
    T(n)=n

    찾고자 하는 값이 배열의 맨 마지막에 저장되어 있거나 아예 저장되어 있지 않은 경우  
    알고리즘 성능을 판단하는데 중요  
 

#### 평균적인 경우
    T(n)=n*3/4

    탐색 대상이 배열에 존재하지 않을 확률 50%라고 가정  
    탐색 대상이 존재하지 않는 경우의 연산 횟수: n   
    탐색 대상이 존재하는 경우의 연산 횟수 n/2   
    계산하기 어려움 
 
<br>

## 이진 탐색 알고리즘   
  
정렬된 데이터가 아니면 적용이 불가능하다   

1. 배열의 중앙에 찾는 값이 저장되어 있는지 확인한다.    
2. 찾는 값이 배열의 중앙에 있는 값보다 크면 탐색의 범위를 배열의 왼쪽 부분으로 제한한다.  
3. 찾는 값이 배열의 중앙에 있는 값보다 작으면 탐색의 범위를 배열의 오른쪽 부분으로 제한한다.  
      2, 3번👉 탐색의 대상을 반으로 줄임  

 
<br>

- 이진 탐색 알고리즘의 구현
```C
int BSearch(int ar[], int len, int target) {
	int first = 0;
	int last = len - 1;
	int mid;
	while (first <= last) { // 탐색의 대상이 존재함
		mid = (first + last) / 2;
		if (target == ar[mid]) {
			return mid;
		}
		else {
			if (target < ar[mid])
				last = mid - 1;
			else
				first = mid + 1;
		}
		return -1;
}
```

### 최악의 경우
    T(n)=log2(n)

    n이 1이 되기 까지 2로 나눈 횟수가 k회, 비교연산 k회 진행  
    데이터가 1개 남았을 때 마지막을 비교연산 1회 진행  
      👉 T(n)=k+1
      👉 n*(1/2)^k=1이므로 k=log2(n)

 
<br>

## 빅오표기법   
함수 T(n)에서 가장 영향력이 큰 부분이 어딘가를 따지는 것  
*O(1) < O(logn) < O(n) < O(nlogn) < O(n^2) < O(n^3) < O(2^n)*

<br>