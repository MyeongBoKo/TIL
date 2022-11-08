# 기수 정렬
- 기수(radix)란 주어진 데이터를 구성하는 기본 요소를 의미
- 데이터를 구성하는 기본 요소, 즉 기수를 이용해서 정렬을 진행하는 방식
- 길이가 같은 데이터들을 대상으로 정렬 가능하지만, 길이가 같지 않은 데이터들을 대상으로 정렬이 불가능하다.

## LSD 정렬
- LSD는 Least Significant Digit의 약자
- 덜 중요한 정렬을 진행해 나가는 의미, 첫 번째 자릿수부터 시작해서 정렬을 진행해 나간다는 의미다.

## MSD 정렬
- MSD는 Most Significant Digti의 약자
- 큰 자릿수에서부터 정렬이 진행된다는 의미
- 점진적으로 정렬을 완성해가는 방식이기 때문에 반드시 끝까지 가지 않아도 중간에 정렬이 완료될 수 있는 장점을 가지고 있다.
- 모든 데이터에 일괄적인 과정을 거치게 할 수 없어서 오류를 범하지 않기 위해서 중간에 데이터를 점검해야 하는 단점을 가지고 있다.
## 헤더파일
```c
#ifndef __LISTBASE_QUEUE_H__
#define __LISTBASE_QUEUE_H__

#define TRUE		1
#define FALSE		0

typedef int Data;

typedef struct __node
{
	Data data;
	struct __node* next;
} Node;

typedef struct __lQueue
{
	Node* front;
	Node* rear;
} LQueue;

typedef LQueue Queue;

void QueueInit(Queue* pq);
int QIsEmpty(Queue* pq);

void Enqueue(Queue* pq, Data data);
Data Dequeue(Queue* pq);
Data QPeek(Queue* pq);

#endif
```

## 소스파일
```c
#include <stdio.h>
#include <stdlib.h>
#include "ListBaseQueue.h"

void QueueInit(Queue* pq)
{
	pq->front = NULL;
	pq->rear = NULL;
}

int QIsEmpty(Queue* pq)
{
	if (pq->front == NULL)
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
		pq->front = newNode;
		pq->rear = newNode;
	}
	else
	{
		pq->rear->next = newNode;
		pq->rear = newNode;
	}
}

Data Dequeue(Queue* pq)
{
	Node* delNode;
	Data retData;

	if (QIsEmpty(pq))
	{
		printf("Queue Memory Error!");
		exit(-1);
	}

	delNode = pq->front;
	retData = delNode->data;
	pq->front = pq->front->next;

	free(delNode);
	return retData;
}

Data QPeek(Queue* pq)
{
	if (QIsEmpty(pq))
	{
		printf("Queue Memory Error!");
		exit(-1);
	}

	return pq->front->data;
}
```

## 메인
```c
#include <stdio.h>
#include "ListBaseQueue.h"

#define BUCKET_NUM		10

void RadixSort(int arr[], int num, int maxLen)
{
	// 매개변수 maxLen에는 정렬대상 중 가장 긴 데이터의 길이 정보가 전달
	Queue buckets[BUCKET_NUM];
	int bi;
	int pos;
	int di;
	int divfac = 1;
	int radix;

	// 총 10개의 버킷 초기화
	for (bi = 0; bi < BUCKET_NUM; bi++)
		QueueInit(&buckets[bi]);

	// 가장 긴 데이터의 길이만큼 반복
	for (pos = 0; pos < maxLen; pos++)
	{
		// 정렬대상의 수만큼 반복
		for (di = 0; di < num; di++)
		{
			// N번째 자리의 숫차 추출
			radix = (arr[di] / divfac) % 10;

			// 추출한 숫자를 근거로 버킷에 데이터 저장
			Enqueue(&buckets[radix], arr[di]);
		}

		// 버킷의 수만큼 반복
		for (bi = 0, di = 0; bi < BUCKET_NUM; bi++)
		{
			// 버킷에 저장된 것 순서대로 다 꺼내서 다시 arr에 저장
			while (!QIsEmpty(&buckets[bi]))
				arr[di++] = Dequeue(&buckets[bi]);
		}

		// N번째 자리의 숫자 추출을 위한 피제수의 증가
		divfac *= 10;
	}
}

int main(void)
{
	int arr[7] = { 13, 212, 14, 7141, 10987,6, 15 };

	int len = sizeof(arr) / sizeof(int);
	int i;

	RadixSort(arr, len, 5);

	for (i = 0; i < len; i++)
		printf("%d ", arr[i]);

	printf("\n");
	return 0;
}
```
# reference
윤성우의 열혈 C 자료구조 - 윤성우
