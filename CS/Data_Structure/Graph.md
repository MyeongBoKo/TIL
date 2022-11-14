# 그래프
## 그래프란
- 정점과 간선을 이용해서 표현한 것을 그래프라고 한다.
- `정점(vertex)`:연결 대상이 되는 개체 또는 위치
- `간선(edge)`: 이들 사이의 연결

## 그래프의 종류
- 무방향 그래프

- 방향 그래프(directed graph) & 다이그래프(digraph)

- 완전 그래프(complete graph)

- 가중치 그래프(Weight graph)

- 부분 그래프(Sub graph)

## 그래프의 ADT
`void GraphInit(UALGraph * pg, int nv);`<br>
- 그래프의 초기화를 진행
- 두 번째 인자로 정점의 수를 전달

`void GraphDestroy(UALGraph * pg);` <br>
- 그래프 초기화 과정에서 할당한 리소스를 반환

`void AddEdge(UALGraph * pg, int fromV, int toV);` <br>
- 매개변수 fromV와 toV로 전달된 정점을 연결하는 간선을 그래프에 추가

`void ShowGraphEdgeInfo(UALGraph * pg);`<br>
- 그래플의 간선정보를 출력

## 구현

### ALGraph.h
```c
#ifndef __AL_GRAPH__
#define __AL_GRAPH__

#include "DLinkedList.h"

// 정점의 이름을 상수화
enum { A, B, C, D, E, F, G, H, I, J };

typedef struct __ual
{
	int numV;
	int numE;
	List* adjList;
} ALGraph;

void GraphInit(ALGraph* pg, int nv);

void GraphDestroy(ALGraph* pg);

void AddEdge(ALGraph* pg, int fromV, int toV);

void ShowGraphEdgeInfo(ALGraph* pg);

#endif
```

### DLinkedList.h
```c
#ifndef __D_LINKED_LIST_H__
#define __D_LINKED_LIST_H__



#define TRUE		1
#define FALSE		0 

typedef int LData;

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


### ALGraph.c
```c
#include <stdio.h>
#include <stdlib.h>
#include "ALGraph.h"
#include "DLinkedList.h"

int WhoIsPrecede(int data1, int data2);

void GraphInit(ALGraph* pg, int nv)
{
	int i;

	pg->adjList = (List*)malloc(sizeof(List) * nv);
	pg->numV = nv;
	pg->numE = 0;
	
	for (i = 0; i < nv; i++)
	{
		ListInit(&(pg->adjList[i]));

		SetSortRule(&(pg->adjList[i]), WhoIsPrecede);
	}
}

void GraphDestory(ALGraph* pg)
{
	if (pg->adjList != NULL)
		free(pg->adjList);
}

void AddEdge(ALGraph* pg, int fromV, int toV)
{
	LInsert(&(pg->adjList[fromV]), toV);
	LInsert(&(pg->adjList[toV]), fromV);
	pg->numE += 1;
}

void ShowGraphEdgeInfo(ALGraph* pg)
{
	int i;
	int vx;

	for (i = 0; i < pg->numV; i++)
	{
		printf("%c와 연결된 장점: ", i + 65);

		if (LFirst(&(pg->adjList[i]), &vx))
		{
			printf("%c ", vx + 65);

			while (LNext(&(pg->adjList[i]), vx))
				printf("%c ", vx + 65);
		}

		printf("\n");
	}
}

int WhoIsPrecede(int data1, int data2)
{
	if (data1 < data2)
		return 0;
	else
		return 1;
}
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

int LFirst(List* plist, LData* pdata)
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

### main
```c
#include <stdio.h>
#include "ALGraph.h"

int main(void)
{
	ALGraph graph;
	GraphInit(&graph, 5);

	AddEdge(&graph, A, B);
	AddEdge(&graph, A, D);
	AddEdge(&graph, A, C);
	AddEdge(&graph, C, D);
	AddEdge(&graph, D, E);
	AddEdge(&graph, E, A);

	ShowGraphEdgeInfo(&graph);
	GraphDestroy(&graph);
	return 0;
}
```

# reference 
윤성우의 열혈 C 자료구조 - 윤성우
