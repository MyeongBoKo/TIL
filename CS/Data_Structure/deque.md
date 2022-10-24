# deque
## deque.h
```c
#ifndef __DEQUE_H__
#define __DEQUE_H__

#define TRUE		1
#define FALSE		0

typedef int Data;

typedef struct __node
{
	Data data;
	struct node* next;
	struct node* prev;
} Node;

typedef struct __dlDeque
{
	Node* head;
	Node* tail;
} DLDeque;

typedef DLDeque Deque;

void DequeInit(Deque* pdeq);
int DQIsEmpty(Deque* pdeq);

void DQAddFirst(Deque* pdeq, Data data);
void DQAddLast(Deque* pdeq, Data data);

Data DQRemoveFirst(Deque* pdeq);
Data DQRemoveLast(Deque* pdeq);

Data DQGetFirst(Deque* pdeq);
Data DQGetLast(Deque* pdeq);

#endif
```

## deque.c
```c
#include <stdio.h>
#include "Deque.h"

void DequeInit(Deque* pdeq)
{
	pdeq->head = NULL;
	pdeq->tail = NULL;
}

int DQIsEmpty(Deque* pdeq)
{
	if (pdeq->head == NULL)
		return TRUE;
	else
		return FALSE;
}

void DQAddFirst(Deque* pdeq, Data data)
{
	Node* newNode = (Node*)malloc(sizeof(Node));
	newNode->data = data;

	newNode->next = pdeq->head;			// dpeq -> head = NULL;

	if (DQIsEmpty(pdeq))
		pdeq->tail = newNode;
	else
		pdeq->head->prev = newNode;

	newNode->prev = NULL;	// 새노드의 prev를 NULL로 초기화
	pdeq->head = newNode;
}

void DQAddLast(Deque* pdeq, Data data)
{
	Node* newNode = (Node*)malloc(sizeof(Node));
	newNode->data = data;

	newNode->prev = pdeq->tail;

	if (DQIsEmpty(pdeq))
		pdeq->head = newNode;
	else
		pdeq->tail->next = newNode;

	newNode->next = NULL;	// 새노드의 next를 NULL로 초기화
	pdeq->tail = newNode;
}

Data DQRemoveFirst(Deque *pdeq)
{
	Node* rnode = pdeq->head;
	Data rdata;
	if (DQIsEmpty(pdeq)) {
		printf("Queue Memory Error!");
		exit(-1);
	}
	rdata = pdeq->head->data;

	pdeq->head = pdeq->head->next;
	free(rnode);

	if (pdeq->head->prev = NULL)
		pdeq->tail = NULL;
	else
		pdeq->head->prev = NULL;

	return rdata;
}

Data DQRemoveLast(Deque* pdeq)
{
	Node* rnode = pdeq->tail;
	Data rdata;
	if (DQIsEmpty(pdeq)) {
		printf("Queue Memory Error!");
		exit(-1);
	}
	rdata = pdeq->tail->data;
	free(rnode);

	if (pdeq->tail == NULL)
		pdeq->head = NULL;
	else
		pdeq->tail->next = NULL;

	return rdata;
}

Data DQGetFirst(Deque* pdeq)
{
	if (DQIsEmpty(pdeq)) {
		printf("Queue Memory Error!");
		exit(-1);
	}

	return pdeq->head->data;
}

Data DQGetLast(Deque* pdeq)
{
	if (DQIsEmpty(pdeq)) {
		printf("Queue Memory Error!");
		exit(-1);
	}

	return pdeq->tail->data;
}
```




# reference 
윤성우의 열혈 자료구조 - 윤성우
