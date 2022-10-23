# 큐
## 배열기반의 큐
### 헤더파일
```c
#ifndef __CIRCULAR_QUEUE_H__
#define __CIRCULAR_QUEUE_H__

#define TRUE		1
#define FALSE		0

#define QUE_LEN		100

typedef int Data;

typedef struct __cQueue
{
	int front;	// 그림에서 F를 표현한 멤버
	int rear;	// 그림에서 R을 표현한 멤버
	Data queArr[QUE_LEN];
} CQUEUE;

typedef CQUEUE Queue;

void QueueInit(Queue* pq);
int QIsEmpty(Queue* pq);

void Enqueue(Queue* pq, Data data);
Data Dequeue(Queue* pq);
Data QPeek(Queue* pq);


#endif
```
### 소스파일
```c
#include <stdio.h>
#include <stdlib.h>
#include "CircularQueue.h"

void QueueInit(Queue* pq)
{
	pq->front = 0;
	pq->rear = 0;
}

int QIsEmpty(Queue* pq)
{
	if (pq->front == pq->rear)
		return TRUE;
	else
		return FALSE;
}

int NextPosIdx(int pos)		// 큐의 다음 위치에 해당하는 인덱스 값 반환
{
	if (pos == QUE_LEN - 1)			// 배열의 한칸은 비움
		return 0;
	else
		return pos + 1;
}

void Enqueue(Queue* pq, Data data)
{
	if (NextPosIdx(pq->rear) == pq->front)	// 큐가 full
	{
		printf("Queue Memory Error!");
		exit(-1);
	}

	pq->rear = NextPosIdx(pq->rear);		// rear을 한 칸 이동
	pq->queArr[pq->rear] = data;			// rear이 가리키는 곳에 데이터 저장
}

Data Dequeue(Queue* pq)
{
	if (QIsEmpty(pq))
	{
		printf("Queue Memory Error!");
		exit(-1);
	}

	pq->front = NextPosIdx(pq->front);		// front를 한 칸 이동
	return pq->queArr[pq->front];			// front가 가리키는 데이터 반환
}

Data QPeek(Queue* pq)
{
	if (QIsEmpty(pq))
	{
		printf("Queue Memory Error!");
		exit(-1);
	}

	return pq->queArr[NextPosIdx(pq->front)];
}
```
### 메인파일
```c
#include <stdio.h>
#include "CircularQueue.h"

int main(void)
{
	Queue q;
	QueueInit(&q);

	Enqueue(&q, 1);
	Enqueue(&q, 2);
	Enqueue(&q, 3);
	Enqueue(&q, 4);
	Enqueue(&q, 5);

	while (!QIsEmpty(&q))
	{
		printf("%d ", Dequeue(&q));
	}

	return 0;
}
```

## 리스트 기반의 큐
### 헤더파일
```c
#ifndef __LB_QUEUE_H__
#define __LB_QUEUE_H__

#define TRUE		1
#define FALSE		0

typedef int Data;

typedef struct __node
{
	Data data;
	struct node* next;
} Node;

typedef struct __lQueue
{
	Node* Front;
	Node* Rear;
} LQueue;

typedef LQueue Queue;

void InitQueue(Queue* pq);
int QIsEmpty(Queue* pq);

void Enqueue(Queue* pq, Data data);
Data Dequeue(Queue* pq);
Data QPeek(Queue* pq);

#endif
```

### 소스파일
```c
#include <stdio.h>
#include "ListBaseQueue.h"

void InitQueue(Queue* pq)
{
	pq->Front = NULL;
	pq->Rear = NULL;
}

int QIsEmpty(Queue* pq)
{
	if (pq->Front == NULL)
		return TRUE;
	else
		return FALSE;
}

void Enqueue(Queue* pq, Data data)
{
	Node* newNode = (Node*)malloc(sizeof(Node));
	newNode->next = NULL;
	newNode->data = data;

	if (QIsEmpty(pq))
	{
		pq->Front = newNode;
		pq->Rear = newNode;
	}
	else
	{
		pq->Rear->next = newNode;	// 마지막 노드가 새 노드를 가리킨다.
		pq->Rear = newNode;
	}
}

Data Dequeue(Queue* pq)
{
	Node* delNode;
	Data rdata;

	if (QIsEmpty(pq))
	{
		printf("Queue Memory Error!");
		exit(-1);
	}
	delNode = pq->Front;
	rdata = delNode->data;
	pq->Front = pq->Front->next;

	free(delNode);
	return rdata;
}

Data QPeek(Queue* pq)
{
	if (QIsEmpty(pq))
	{
		printf("Queue Memory Error!");
		exit(-1);
	}

	return pq->Front->data;
}
```

### main
```c
#include <stdio.h>
#include "ListBaseQueue.h"

int main(void)
{
	Queue q;
	InitQueue(&q);

	Enqueue(&q, 1);
	Enqueue(&q, 2);
	Enqueue(&q, 3);
	Enqueue(&q, 4);
	Enqueue(&q, 5);

	while (!QIsEmpty(&q))
	{
		printf("%d ", Dequeue(&q));
	}
	
	return 0;
}
```

## 큐의 활용
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include "CircularQueue.h"

#define CUS_COME_TERM		15

#define CHE_BURG			0
#define BUL_BURG			1
#define DBL_BURG			2

#define CHE_BURG_TIME		12
#define BUL_BURG_TIME		15
#define DBL_BURG_TIME		24

int main(void)
{
	int makepro = 0;	// 햄버거 주문 상황
	int cheOrder = 0, bulOrder = 0, dblOrder = 0;
	int sec;

	Queue q;

	InitQueue(&q);
	srand(time(NULL));

	for (sec = 0; sec < 3600; sec++)
	{
		if (sec % CUS_COME_TERM == 0)
		{
			switch (rand() % 3)
			{
			case CHE_BURG:
				Enqueue(&q, CHE_BURG_TIME);
				cheOrder += 1;
				break;

			case BUL_BURG:
				Enqueue(&q, BUL_BURG_TIME);
				bulOrder += 1;
				break;

			case DBL_BURG:
				Enqueue(&q, DBL_BURG_TIME);
				dblOrder += 1;
				break;
			}
		}

		if (makepro <= 0 && !QIsEmpty(&q))
			makepro = Dequeue(&q);

		makepro--;
	}

	printf("Simulation Report!\n");
	printf(" - Cheese burger: %d\n");
	printf(" - Bulgogi burger: %d\n");
	printf(" - Double burger: %d\n");
	printf(" - Waiting Room size: %d \n", QUE_LEN);
}
```


# reference 
윤성우의 열혈 자료구조 - 윤성우
