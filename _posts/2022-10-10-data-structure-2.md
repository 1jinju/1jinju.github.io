---
layout: post
title: Ch 2. 재귀
subtitle: 윤성우의 열혈 자료구조
cover-img: /assets/img/black.jpg
thumbnail-img: https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcil3sy%2Fbtrtlaaou9Z%2FOzKxEzB0Hv3rrEhxVR7GEk%2Fimg.png
share-img: /assets/img/path.jpg
tags: [자료구조]
---

# 02-1 함수의 재귀적 호출의 이해

## 재귀

재귀함수: 함수가 호출되면 해당 함수의 복사본을 만들어서 실행하는 구조

```c
void Recursive(int num) {
	if (num <= 0) // 재귀의 탈출 조건
		return;
	printf("Recursive call! %d \n", num);
	Recursive(num-1);
}
```
<br>

## 팩토리얼

n! = n * (n-1) * (n-2) * ... * 2 * 1   
(n-1)! = (n-1) * (n-2) * (n-3) * ... * 2 * 1   
n! = n*(n-1)!   

| f(n) | n * f(n-1) | n ≥ 1 |
| --- | --- | ---  |
|     |  1  | n = 0 |

<br>

```c
int Factorial(int n) {
	if (n == 0) // 탈출조건
		return 1;
	else
		return n * Factorial(n-1);
}
```

<br>

---

# 02-2 재귀의 활용

## 피보나치 수열

앞의 것 두 개를 더해서 현재의 수를 만들어가는 재귀적인 형태를 띠는 대표적인 수열

```c
int Fibo(int n) {
	if (n == 1)
		return 0;
	else if (n == 2)
		return 1;
	else
		return Fibo(n-1) + Fibo(n-2);
}
```

![재귀함수 호출 구조](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcil3sy%2Fbtrtlaaou9Z%2FOzKxEzB0Hv3rrEhxVR7GEk%2Fimg.png)

👉 재귀함수는 많은 수의 함수 호출을 동반

<br>


## 이진 탐색 알고리즘의 재귀적 구현

- 동일한 패턴 반복(재귀적인 성격)
    1. 탐색 범위의 중앙에 목푯값이 저장되었는지 확인
    2. 저장되지 않았다면 탐색 범위를 반으로 줄여서 다시 탐색 시작
- 탈출조건  
     - 탐색 범위의 시작위치 first가 탐색 범위의 끝 last보다 커지는 경우
    

```c
int BSearchRecur(int ar[], int first, int last, int target) {
	int mid;
	if (first > last)
		return -1;
	mid = (first + last) / 2;

	if (ar[mid] == target)
		return mid;
	else if (target < ar[mid])
		return BSearchRecur(ar, first, mid-1, target)
	else
		return BSearchRecur(ar, mid+1, last, target)
}
```

<br>

---

# 02-3 하노이 타워

하나의 막대에 쌓여 있는 원반을 다른 하나의 원반에 그대로 옮기는 방법  
원반은 한 번에 하나씩만 옮길 수 있다.  
옮기는 과정에서 작은 원반의 위에 큰 원반이 올려져서는 안 된다.  

## 반복 패턴(재귀적으로 구성)

1. 작은 원반 n-1개를 A에서 B로 이동
2. 큰 원반 1개를 A에서 C로 이동
3. 작은 원반 n-1개를 B에서 C로 이동

탈출조건: 이동해야 할 원반의 수가 1개인 경우

👉 원반 n개를 이동하는 문제는 결국 원반 1개를 이동하는 매우 쉬운 문제로 세분화

```c
void HanoiTowerMove(int num, char from, char by, char to) {
	if (num == 1) {
		printf("원반1을 %c에서 %c로 이동 \n", from, to);
	}
	else{
		HanoiTowerMove(num-1, from, to, by)
		printf("원반 %d을(를) %c에서 %c로 이동 \n", num, from, to);
		HanoiTowerMove(num-1, by, from, to);
	}
}
```

- 파이썬

```python
def HanoiTowerMove(num, fr, by, to):
    if num == 1:
        print("원반 1을 %c에서 %c로 이동" %(fr, to))
    else:
        HanoiTowerMove(num-1, fr, to, by)
        print("원반 %d을(를) %c에서 %c로 이동" %(num, fr, to))
        HanoiTowerMove(num-1, by, fr, to)

HanoiTowerMove(3, 'A', 'B', 'C')
```

<br>