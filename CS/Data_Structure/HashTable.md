# 테이블과 해쉬
## 테이블
- 저장된 데이터는 키(key)와 값(Value)이 하나의 쌍을 이룸
- 키가 존재하지 않는 값은 저장 불가, 모든 키는 중복 불가
- 자료구조의 테이블은 사전구조 그리고 맵이라 불린다.
- 테이블은 고유번호의 범위가 배열의 인덱스 값으로 사용하기 힘들고, 범위를 수용할 수 있는 매우 큰 배열이 필요하다는 단점을 가지고 있다.

## 해쉬 함수
- 테이블의 단점을 해결한 것을 해쉬 함수라 한다.
- 넓은 범위의 키를 좁은 범위의 키로 변경
- 해쉬 함수를 통해 범위가 좁아지는데, 이때 값이 같은 문제가 발생
- 이것 문제를 충돌(Collision)이라 한다.
- 충돌은 피하는 것이 아니라 해결해야 한다.

## 충돌 문제의 해결책
### 선형조사법 & 이차 조사법
- 선형조사법은 충돌이 발생했을 때, 옆자리가 비었는지 확인하고 비어있으면 그 자리에 대신 저장하는 방법이다.
- f(k)+1 -> f(k)+2 -> f(k)+3 -> f(k)+4 ...
- 선형 조사법의 경우 충돌의 횟수가 증가함에 따라서 클러스터 현상(특정 영역에 데이터가 몰리는 현상)이 발생

### 이차 조사법
- 이차 조사법은 선형 조사법에서 발생하는 클러스터 현상을 보완한 방법이다.
- f(k) + 1^2 -> f(k) + 2^2 -> f(k) + 3^2 -> f(k) + 4^2 ... 
- 해쉬 값이 같으면 빈 슬롯을 찾아서 접근하는 위치가 동일하다는 단점을 가지고 있다.

### 이중 해쉬
- 두 개의 해쉬 함수를 이용해서 위의 조사법의 단점을 보완
- 1차 해쉬 함수: 키를 근거로 저장위치를 결정하기 위한 것
- 2차 해쉬 함수: 충돌 발생시 몇 칸 뒤를 살필지 결정하기 위한 것

### 배열을 기반으로 하는 테이블
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

typedef struct __empInfo
{
	int empNum;									// 직원의 고유번호
	int age;									// 직원의 나이
} EmpInfo;

int main(void)
{
	EmpInfo empInfoArr[1000];					// 직원들의 정보를 저장하기 위해 선언된 배열
	EmpInfo ei;
	int eNum;

	printf("사번과 나이 입력: ");
	scanf("%d %d", &(ei.empNum), &(ei.age));
	empInfoArr[ei.empNum] = ei;					// 저장 

	printf("확인하고픈 직원의 사번 입력: ");
	scanf("%d", &eNum);

	ei = empInfoArr[eNum];						// 탐색
	printf("사번 %d, 나이 %d \n", ei.empNum, ei.age);
	return 0;
}
```
### 해쉬 기능이 있는 테이블
```c
#include <stdio.h>

typedef struct __empInfo
{
	int empNum;
	int age;
} EmpInfo;

int GetHashValue(int empNum)
{
	return empNum % 100;
}

int main(void)
{
	EmpInfo empInfoArr[100];

	EmpInfo emp1 = { 20120003, 42 };
	EmpInfo emp2 = { 20130012, 33 };
	EmpInfo emp3 = { 20170049, 27 };

	EmpInfo r1, r2, r3;

	// 키를 인덱스 값으로 이용해서 저장
	empInfoArr[GetHashValue(emp1.empNum)] = emp1;
	empInfoArr[GetHashValue(emp2.empNum)] = emp2;
	empInfoArr[GetHashValue(emp3.empNum)] = emp3;

	// 키를 인덱스 값으로 이용해서 탐색
	r1 = empInfoArr[GetHashValue(20120003)];
	r2 = empInfoArr[GetHashValue(20130012)];
	r3 = empInfoArr[GetHashValue(20170049)];

	// 탐색 결과 확인
	printf("% 사번 %d, 나이 %d \n", r1.empNum, r1.age);
	printf("% 사번 %d, 나이 %d \n", r2.empNum, r2.age);
	printf("% 사번 %d, 나이 %d \n", r3.empNum, r3.age);
	
}
```
## 해쉬&테이블 구현
### Person.h
```c
#ifndef __PERSON_H__
#define __PERSON_H__

#define STR_LEN		50

typedef struct __person
{
	int ssn;				// 주민번호
	char name[STR_LEN];		// 이름
	char addr[STR_LEN];		// 주속
} Person;

int GetSSN(Person* p);

void ShowPerInfo(Person* p);

Person* MakePersonData(int ssn, char* name, char* addr);

#endif
```

### Slot.h
```c
#ifndef __SLOT_H__
#define __SLOT_H__

#include "Person.h"

typedef int Key;			// 주민등록번호
typedef Person* Value;		// Person 구조체 변수의 주소값

enum SlotStatus{EMPTY, DELETED, INUSE};

typedef struct __slot
{
	Key key;
	Value val;
	enum SlotStatus status;
} Slot;

#endif
```

### Table.h
```c
#ifndef __TABLE_H__
#define __TABLE_H__

#include "Slot.h"

#define MAX_LEN		100

typedef int (HashFunc)(Key k);

typedef struct __table
{
	Slot tbl[MAX_LEN];
	HashFunc* hf;
} Table;

// 테이블의 초기화
void TBLInit(Table* pt, HashFunc* f);

// 테이블에 키와 값을 저장
void TBLInsert(Table* pt, Key k, Value v);

// 키를 근거로 테이블에서 데이터 삭제
Value TBLDelete(Table* pt, Key k);

// 키를 근거로 테이블에서 데이터 탐색
Value TBLSearch(Table* pt, Key k);

#endif
```


### Person.c
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include "Person.h"

int GetSSN(Person* p)
{
	return p->ssn;
}

void ShowPerInfo(Person* p)
{
	printf("주민등록번호: %d \n", p->ssn);
	printf("이름: %s \n", p->name);
	printf("주소: %s \n\n", p->addr);
}

Person* MakePersonData(int ssn, char* name, char* addr)
{
	Person* newP = (Person*)malloc(sizeof(Person));
	newP->ssn = ssn;
	strcpy(newP->name, name);
	strcpy(newP->addr, addr);
	return newP;
}
```
### Table.c
```c
#include <stdio.h>
#include <stdlib.h>
#include "Table.h"

void TBLInit(Table* pt, HashFunc* f)
{
	int i;

	// 모든 슬롯 초기화
	for (i = 0; i < MAX_LEN; i++)
		(pt->tbl[i]).status = EMPTY;

	pt->hf = f;		// 해쉬 함수 등록
}

void TBLInsert(Table* pt, Key k, Value v)
{
	int hv = pt->hf(k);
	pt->tbl[hv].val = v;
	pt->tbl[hv].key = k;
	pt->tbl[hv].status = INUSE;
}

Value TBLDelete(Table* pt, Key k)
{
	int hv = pt->hf(k);

	if ((pt->tbl[hv]).status != INUSE)
	{
		return NULL;
	}
	else
	{
		(pt->tbl[hv]).status = DELETED;
		return (pt->tbl[hv]).val;
	}
}

Value TBLSearch(Table* pt, Key k)
{
	int hv = pt->hf(k);

	if ((pt->tbl[hv]).status != INUSE)
		return NULL;
	else
		return (pt->tbl[hv]).val;
}
```

### 메인
```c
#include <stdio.h>
#include <stdlib.h>
#include "Person.h"
#include "Table.h"

int MyHashFunc(int k)
{
	return k % 100;
}

int main(void)
{
	Table myTbl;
	Person* np;
	Person* sp;
	Person* rp;

	TBLInit(&myTbl, MyHashFunc);

	// 데이터 입력
	np = MakePersonData(20120003, "Lee", "Seoul");
	TBLInsert(&myTbl, GetSSN(np), np);

	np = MakePersonData(20130012, "KIM", "Jeju");
	TBLInsert(&myTbl, GetSSN(np), np);

	np = MakePersonData(20170049, "HAN", "Jenju");
	TBLInsert(&myTbl, GetSSN(np), np);

	// 데이터 탐색
	sp = TBLSearch(&myTbl, 20120003);
	if (sp != NULL)
		ShowPerInfo(sp);

	sp = TBLSearch(&myTbl, 20130012);
	if (sp != NULL)
		ShowPerInfo(sp);
	
	sp = TBLSearch(&myTbl, 20170049);
	if (sp != NULL)
		ShowPerInfo(sp);

	// 데이터 삭재
	rp = TBLDelete(&myTbl, 20120003);
	if (rp != NULL)
		free(rp);

	rp = TBLDelete(&myTbl, 20130012);
	if (rp != NULL)
		free(rp);

	rp = TBLDelete(&myTbl, 20170049);
	if (rp != NULL)
		free(rp);

	return 0;

}
```

## 체이닝
### DLinkedList.h
```c
#ifndef __D_LINKED_LIST_H__
#define __D_LINKED_LIST_H__

#include "Slot2.h"

#define TRUE		1
#define FALSE		0 

typedef Slot LData;

typedef struct __node
{
	LData data;
	struct __node* next;
} Node;

typedef struct __linkedList
{
	Node* head;
	Node* cur;
	Node* before;
	int numOfData;
	int (*comp)(LData d1, LData d2);
} LinkedList;

typedef LinkedList List;

void ListInit(List* plist);
void LInsert(List* plist, LData data);

int LFirst(List* plist, LData* pdata);
int LNext(List* plist, LData* pdata);

LData LRemove(List* plist);
int LCount(List* plist);

void SetSortRule(List* plist, int(*comp)(LData d1, LData d2));

#endif
```

### Person.h
```c
#ifndef __PERSON_H__
#define __PERSON_H__

#define STR_LEN		50

typedef struct __person
{
	int ssn;				// 주민번호
	char name[STR_LEN];		// 이름
	char addr[STR_LEN];		// 주속
} Person;

int GetSSN(Person* p);

void ShowPerInfo(Person* p);

Person* MakePersonData(int ssn, char* name, char* addr);

#endif
```

### Table2.h
```c
#ifndef __TABLE2_H__
#define __TABLE2_H__

#include "Slot2.h"
#include "DLinkedList.h"

#define MAX_TBL		100

typedef int (HashFunc)(Key k);

typedef struct __table
{
	List tbl[MAX_TBL];
	HashFunc* hf;
} Table;

// 테이블의 초기화
void TBLInit(Table* pt, HashFunc* f);

// 테이블에 키와 값을 저장
void TBLInsert(Table* pt, Key k, Value v);

// 키를 근거로 테이블에서 데이터 삭제
Value TBLDelete(Table* pt, Key k);

// 키를 근거로 테이블에서 데이터 탐색
Value TBLSearch(Table* pt, Key k);

#endif 
```

### Slot2.h
```c
#ifndef __SLOT2_H__
#define __SLOT2_H__

#include "Person.h"

typedef int Key;
typedef Person* Value;

typedef struct __slot
{
	Key key;
	Value val;
} Slot;

#endif
```

### DLinkedList.c
```c
#include <stdio.h>
#include <stdlib.h>
#include "DLinkedList.h"

void ListInit(List* plist)
{
	plist->head = (Node*)malloc(sizeof(Node));
	plist->head->next = NULL;
	plist->comp = NULL;
	plist->numOfData = 0;
}

void FInsert(List* plist, LData data)
{
	Node* newNode = (Node*)malloc(sizeof(Node));
	newNode->data = data;

	newNode->next = plist->head->next;
	plist->head->next = newNode;

	(plist->numOfData)++;
}

void SInsert(List* plist, LData data)
{
	Node* newNode = (Node*)malloc(sizeof(Node));
	Node* pred = plist->head;
	newNode->data = data;

	while (pred->next != NULL && plist->comp(data, pred->next->data) != 0)
	{
		pred = pred->next;
	}

	newNode->next = pred->next;
	pred->next = newNode;

	(plist->numOfData)++;
}

void LInsert(List* plist, LData data)
{
	if (plist->comp == NULL)
		FInsert(plist, data);
	else
		SInsert(plist, data);
}

int LFirst(List* plist, LData *pdata)
{
	if (plist->head->next == NULL)
		return FALSE;

	plist->before = plist->head;
	plist->cur = plist->head->next;

	*pdata = plist->cur->data;
	return TRUE;
}

int LNext(List* plist, LData* pdata)
{
	if (plist->cur->next == NULL)
		return FALSE;

	plist->before = plist->cur;
	plist->cur = plist->cur->next;

	*pdata = plist->cur->data;
	return TRUE;
}

LData LRemove(List* plist)
{
	Node* rpos = plist->cur;
	LData rdata = rpos->data;

	plist->before->next = plist->cur->next;
	plist->cur = plist->before;

	free(rpos);
	(plist->numOfData)--;
	return rdata;
}

int LCount(List* plist)
{
	return plist->numOfData;
}

void SetSortRule(List* plist, int (*comp)(LData d1, LData d2))
{
	plist->comp = comp;
}
```

### Person2.c
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include "Person.h"

int GetSSN(Person* p)
{
	return p->ssn;
}

void ShowPerInfo(Person* p)
{
	printf("주민등록번호: %d \n", p->ssn);
	printf("이름: %s \n", p->name);
	printf("주소: %s \n\n", p->addr);
}

Person* MakePersonData(int ssn, char* name, char* addr)
{
	Person* newP = (Person*)malloc(sizeof(Person));
	newP->ssn = ssn;
	strcpy(newP->name, name);
	strcpy(newP->addr, addr);
	return newP;
}
```

### Table2.c
```c
#include <stdio.h>
#include <stdlib.h>
#include "Table2.h"
#include "DLinkedList.h"

void TBLInit(Table* pt, HashFunc* f)
{
	int i;

	for (i = 0; i < MAX_TBL; i++)
		ListInit(&(pt->tbl[i]));

	pt->hf = f;
}

void TBLInsert(Table* pt, Key k, Value v)
{
	int hv = pt->hf(k);
	Slot ns = { k,v };

	if (TBLSearch(pt, k) != NULL)
	{
		printf("키 중복 오류 발생 \n");
		return;
	}
	else
	{
		LInsert(&(pt->tbl[hv]), ns);
	}
}

Value TBLDelete(Table* pt, Key k)
{
	int hv = pt->hf(k);
	Slot cSlot;

	if (LFirst(&(pt->tbl[hv]), &cSlot))
	{
		if (cSlot.key == k)
		{
			LRemove(&(pt->tbl[hv]));
			return cSlot.val;
		}
		else
		{
			while (LNext(&(pt->tbl[hv]), &cSlot))
			{
				if (cSlot.key == k)
				{
					LRemove(&(pt->tbl[hv]));
					return cSlot.val;
				}
			}
		}
	}

	return NULL;
}

Value TBLSearch(Table* pt, Key k)
{
	int hv = pt->hf(k);
	Slot cSlot;

	if (LFirst(&(pt->tbl[hv]), &cSlot))
	{
		if (cSlot.key == k)
		{
			return cSlot.val;
		}
		else
		{
			while (LNext(&(pt->tbl[hv]), &cSlot))
			{
				if (cSlot.key == k)
					return cSlot.val;
			}
		}
	}

	return NULL;
}
```

# reference 
윤성우의 열혈 자료구조 - 윤성우
