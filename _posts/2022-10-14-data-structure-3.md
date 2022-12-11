---
layout: post
title: Ch 3. 연결 리스트 1
subtitle: 윤성우의 열혈 자료구조
cover-img: /assets/img/black.jpg
thumbnail-img: https://korenainthekitchen.com/wp-content/uploads/2011/02/white.jpg
share-img: /assets/img/path.jpg
tags: [자료구조]
---

# 03-1 추상 자료형
  
## 자료구조에서의 추상자료형


```
💡 구체적인 기능의 완성과정을 언급하지 않고, 순수하게 기능이 무엇인지를 나열한 것
```

구조체와 관련된 연산의 종류를 결정하는 것도 자료형 정의의 일부로 보아야 함
<br>
예) 지갑 구조체 + 그 구조체와 관련된 돈을 꺼내는 연산 ⇒ 자료형의 정의 완성

<br>

---

# 03-2 배열을 이용한 리스트의 구현
## 리스트 
- 구현방법에 따라    
    순차리스트: 배열 기반으로 구현  
    연결리스트: 메모리의 동적할당 기반으로 구현
    
- 특성  
    데이터를 나란히 저장한다.  
    중복된 데이터 저장을 허용한다.

<br> 

## 리스트의 ADT

```c
void ListInit(List *plist);
```

초기화할 리스트의 주소 값을 인자로 전달  
리스트 생성 후 제일 먼저 호출되어야 함  

```c
void LInsert(List *plist, LData data);
```

리스트에 데이터 저장  
매개변수 data에 전달된 값 저장  

```c
int LFirst(List *plist, LData *pdata);
```

첫 번째 데이터가 pdata가 가리키는 메모리에 저장됨  
데이터의 참조를 위한 초기화  
참조 성공 시 TRUE(1), 실패 시 FALSE(0) 반환  

```c
int LNext(List *plist, LData *pdata);
```

참조된 데이터 다음 데이터가 pdata가 가리키는 메모리에 저장됨  
순차적인 참조를 위해 반복적인 호출이 가능하다  
참조를 새로 시작하려면 LFirst 함수를 호출해야 함  
참조 성공 시 TRUE(1), 실패 시 FALSE(0) 반환  

```c
LData LRemove(List *plist);
```

LFirst 또는 LNext 함수의 마지막 반환 데이터 삭제  
삭제된 데이터는 반환됨  
연이은 반복 호출을 허용하지 않음  

```c
int LCount(List *plist);
```

리스트에 저장되어 있는 데이터 수 반환   
  
### 데이터의 참조 방식

*LFirst → LNext → LNext → LNext ...*

데이터의 참조위치를 기록하여 LNext 함수를 호출할 때마다 다음에 저장된 데이터를 얻을 수 있다.   
처음부터 참조를 새롭게 시작하기 위해서는 LFirst 함수가 필요하다.   

<br>

## 리스트의 구현

- 헤더파일

```c
typedef struct __ArrayList {
	LData arr[LIST_LEN];
	int numOfData;
	int curPosition;
} ArrayList;

typedef ArrayList List;

void ListInit(List *plist); // 초기화
void LInsert(List *plist, LData data); // 데이터 저장

int LFirst(List *plist, LData *pdata); // 첫 데이터 참조
int LNext(List *plist, LData *pdata); // 두 번째 이후 데이터 참조

LData LRemove(List *plist); // 참조한 데이터 삭제
int LCount(List *plist); // 저장된 데이터의 수 반환
```

- 함수 정의

```c
void ListInit(List *plist) {
	(plist -> numOfData) = 0; // 리스트에 저장된 데이터 수 0
	(plist -> curPosition) = -1; // 현재 아무 위치도 가리키지 않음
}
```

```c
void LInsert(List *plist, LData data) {
	if (plist -> numOfData >= LIST_LEN) {
		puts("저장 불가능");
		return;
	}
	plist -> arr[plist->numOfData] = data; // 데이터 저장
	(plist -> numOfData)++;
}
```

```c
int LFirst(List *plist, LData *pdata) {
	if (plist -> numOfData == 0) // 저장된 데이터가 하나도 없다면
		return FALSE;
	(plist -> curPosition) = 0; // 참조 위치 초기화
	*pdata = plist -> arr[0];
	return TRUE;
}
```

```c
int LNext(List *plist, LData *pdata) {
	if (plist -> curPosition >= (plist -> numOfData) - 1) // 더는 참조할 데이터가 없다면
		return FALSE;
	(plist -> curPosition)++;
	*pdata = plist -> arr[plist->curPosition];
	return TRUE;
}
```

```c
LData LRemove(List *plist) {
	LData rdata = plist -> arr[rpos]; // 삭제할 데이터 임시 저장
	for (i = rpos; i < num - 1; i++) // 데이터 이동
		plist -> arr[i] = plist -> arr[i+1];
	(plist -> numOfData)--;
	(plist -> curPosition)--;
	return rdata;
}
```

중간에 데이터가 삭제되면 뒤의 데이터들을 한칸씩 앞으로 이동시켜 빈 공간을 메워야 한다.

<br>

## 리스트에 구조체 변수 저장하기

리스트에 저장한 데이터가 동적으로 할당된 구조체 변수의 주소 값이라면  
👉 free 함수를 통한 메모리의 해제 과정을 거쳐야 함

<br>

## 배열 기반 리스트의 장점과 단점

- 장점  
    데이터의 참조가 쉽다.  
    인덱스 값을 기준으로 어디든 한 번에 참조가 가능하다.  
    
- 단점  
    배열의 길이가 초기에 결정되어야 하고, 변경이 불가능하다.  
    삭제 과정에서 데이터 이동(복사)이 빈번히 일어난다.  

<br>
