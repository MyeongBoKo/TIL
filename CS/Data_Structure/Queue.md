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

int NextPosIdx(int pos)
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

# reference 
윤성우의 열혈 자료구조 - 윤성우
