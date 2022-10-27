# 양방향 연결 리스트

## 헤더파일
```c
#ifndef __DB_LINKED_LIST__
#define __DB_LINKED_LIST__

#define TRUE	1
#define FALSE	0

typedef int Data;

typedef struct __node
{
	Data data;
	struct __node* next;
	struct __node* prev;
} Node;

typedef struct __DLinkedList
{
	Node* head;
	Node* cur;
	int numOfData;
} DBLinkedList;

typedef DBLinkedList List;

void ListInit(List* plist);
void LInsert(List* plist, Data data);

int LFirst(List* plist, Data* pdata);
int LNext(List* plist, Data* pdata);
int LPrevious(List* plist, Data* pdata);
int LCount(List* plist);

#endif
```

## 소스파일
```c
#include <stdio.h>
#include <stdlib.h>
#include "DBLinkedList.h"

void ListInit(List* plist)
{
	plist->head = NULL;
	plist-> numOfData = 0;
}

void LInsert(List* plist, Data data)
{
	Node* newNode = (Node*)malloc(sizeof(Node));
	newNode->data = data;

	newNode->next = plist->head;
	if (plist->head != NULL)
		plist->head->prev = newNode;

	newNode->prev = NULL;
	plist->head = newNode;

	(plist->numOfData)++;
}

int LFirst(List* plist, Data* pdata)
{
	if (plist->head == NULL)
		return FALSE;

	plist->cur = plist->head;	// cur이 첫 번째 노드를 가리킴
	*pdata = plist->cur->data;

	return TRUE;
}

int LNext(List* plist, Data* pdata)
{
	if (plist->cur->next == NULL)
		return FALSE;

	plist->cur = plist->cur->next;	// cur을 오른쪽으로 이동
	*pdata = plist->cur->data;		
	return TRUE;
}

int LPrevious(List* plist, Data* pdata)
{
	if (plist->cur->prev == NULL)
		return FALSE;

	plist->cur = plist->cur->prev;	// cur을 왼쪽으로 이동
	*pdata = plist->cur->data;
	return TRUE;
}

int LCount(List* plist)
{
	return plist->numOfData;
}
```

## 메인파일
```c
#include <stdio.h>
#include "DBLinkedList.h"

int main(void)
{
	List list;
	int data;
	ListInit(&list);

	LInsert(&list, 1);	LInsert(&list, 2);
	LInsert(&list, 3);	LInsert(&list, 4);
	LInsert(&list, 5);	LInsert(&list, 6);
	LInsert(&list, 7);	LInsert(&list, 8);

	if (LFirst(&list, &data)) {
		printf("%d ", data);

		// 오른쪽으로 이동하면서 조회
		while (LNext(&list, &data))
			printf("%d ", data);

		// 왼쪽으로 이동하면서 조회
		while (LPrevious(&list, &data))
			printf("%d ", data);

		printf("\n\n");
	}

	return 0;
}

/*
8 7 6 5 4 3 2 1 2 3 4 5 6 7 8
*/
```

## 더미 노드 기반의 양방향 연결 리스트
### 헤더
```c
#ifndef __DB_LINKED_LIST_H__
#define __DB_LINKED_LIST_H__

#define TRUE		1
#define FALSE		0

typedef int Data;

typedef struct __node
{
	Data data;
	struct __node* next;
	struct __node* prev;
} Node;

typedef struct __dbDLinkedList
{
	Node* head;
	Node* tail;
	Node* cur;
	int numOfData;
} DBDLinkedList;

typedef DBDLinkedList List;

void ListInit(List* plist);
void LInsert(List* plist, Data data);

int LFirst(List* plist, Data* pdata);
int LNext(List* plist, Data* pdata);

Data LRemvoe(List* plist);
int LCount(List* plist);

#endif
```
### 소스
```c
#include <stdio.h>
#include "DBDLinkedList.h"

void ListInit(List* plist)
{
	plist->head = (Node*)malloc(sizeof(Node));
	plist->tail = (Node*)malloc(sizeof(Node));

	plist->head->prev = NULL;
	plist->head->next = plist->tail;

	plist->tail->next = NULL;
	plist->tail->prev = plist->head;

	plist->numOfData = 0;
}

void Linsert(List* plist, Data data)
{
	Node* newNode = (Node*)malloc(sizeof(Node));
	newNode->data = data;

	newNode->prev = plist->tail->prev;
	plist->tail->prev->next = newNode;

	newNode->next = plist->tail;
	plist->tail->prev = newNode;

	(plist->numOfData)++;
}

int LFirst(List* plist, Data* pdata)
{
	if (plist->head->next == plist->tail)
		return FALSE;

	plist->cur = plist->head->next;
	*pdata = plist->cur->data;
	return TRUE;
}

int LNext(List* plist, Data* pdata)
{
	if (plist->cur->next == plist->tail)
		return FALSE;

	plist->cur = plist->cur->next;
	*pdata = plist->cur->data;
	return TRUE;
}

Data LRemove(List* plist)
{
	Node* rpos = plist->cur;
	Data rdata = plist->cur->data;

	plist->cur->prev->next = plist->cur->next;
	plist->cur->next->prev = plist->cur->prev;

	plist->cur = plist->cur->prev;

	free(rpos);
	(plist->numOfData)--;
	return rdata;
}

int LCount(List* plist)
{
	return plist->numOfData;
}
```


# reference 
윤성우의 열혈 자료구조 - 윤성우
