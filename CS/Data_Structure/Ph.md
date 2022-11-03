# 우선순위 큐

## 힙
- 힙은 이진 트리면서 완전 이진 트리다.
- 모든 노드에 저장된 값은 자식 노드에 저장된 값보다 크거나 같아야 한다.
- `최대 힙`이란 루트 노드로 올라갈수록 저장된 값이 커지는 완전 이진 트리
- `최소 힙`이란 루트 노드로 올라갈수록 저장된 값이 작아지는 와전 이진 트리

### 힙에서의 데이터 저장과정
1. 새로운 데이터는 우선순위가 가장 낮다는 가정하에 완전 이진 트리가 유지되는 마지막 노드에 위치시킨다.

2. 부모 노드와 비교해서 우선순위가 높다면 위치를 변경시킨다.
3. 마지막까지 비교시킨 후 최종 결과를 도출시킨다.

### 힙에서의 데이터 삭제과정
- 힙에서 루트 노드를 삭제한 다음 채우는 과정
1. 마지막 노드를 루트 노드의 자리로 옮긴다.

2. 자식 노드와 비교하면서 위치를 변경시킨다.
3. 위치를 변경시킬 수 없는 순간이 올 때까지 비교한 후 최종 결과를 도출시킨다.

### 배열을 기반으로 힙을 구현하는데 필요한 지식
- 노드에 고유의 번호는 각 노드의 데이터가 저장될 배열의 인덱스 값
- 인덱스가 0인 위치의 배열 요소를 사용하지 않는다.

- 왼쪽 자식노드 & 오른쪽 자식노드 & 부모 노드의 인덱스 값을 얻는 방법
  - 왼쪽 자식 노드의 인덱스 값: 부모 노드의 인덱스 값 * 2
  
  - 오른쪽 자식 노드의 인덱스 값: 부모 노드의 인덱스 값*2 + 1
  - 부모 노드의 인덱스 값: 자식 노드의 인덱스 값/2

### 헤더파일
```c
#ifndef __SIMPLE_HEAP_H__
#define __SIMPLE_HEAP_H__

#define TRUE		1
#define FALSE		0

#define HEAP_LEN	100

typedef char HData;
typedef int Priority;

typedef struct _heapElem
{
	Priority pr;
	HData data;
} HeapElem;

typedef struct __heap
{
	int numOfData;
	HeapElem heapArr[HEAP_LEN];
} Heap;

void HeapInit(Heap* ph);

int HIsEmpty(Heap* ph);

void HInsert(Heap* ph, HData data, Priority pr);
HData HDelete(Heap* ph);

#endif
```

### 소스파일
```c
#include "SimpleHeap.h"

void HeapInit(Heap* ph)
{
	ph->numOfData = 0;
}

int HIsEmtpy(Heap* ph)
{
	if (ph->numOfData == 0)
		return TRUE;
	else
		return FALSE;
}

int GetParentIDX(int idx)
{
	return idx / 2;
}

int GetLChildIDX(int idx)
{
	return idx * 2;
}

int GetRChildIDX(int idx)
{
	return GetLChildIDX(idx) + 1;
}

int GetHiPriChildIDX(Heap* ph, int idx)
{
	if (GetLChildIDX(idx) > ph->numOfData)
		return 0;
	else if (GetLChildIDX(idx) == ph->numOfData)
		return GetLChildIDX(idx);
	else
	{
		if (ph->heapArr[GetLChildIDX(idx)].pr > ph->heapArr[GetRChildIDX(idx)].pr)
			return GetRChildIDX(idx);
		else
			return GetLChildIDX(idx);
	}
}

void HInsert(Heap* ph, HData data, Priority pr)
{
	int idx = ph->numOfData + 1;
	HeapElem nelem = { pr, data };

	while (idx != 1)
	{
		if (pr < (ph->heapArr[GetParentIDX(idx)].pr))
		{
			ph->heapArr[idx] = ph->heapArr[GetParentIDX(idx)];
			idx = GetParentIDX(idx);
		}
		else
			break;
	}

	ph->heapArr[idx] = nelem;
	ph->numOfData += 1;
}

HData HDelete(Heap* ph)
{
	HData retData = (ph->heapArr[1]).data;
	HeapElem lastElem = ph->heapArr[ph->numOfData];

	int parentIdx = 1;
	int childIdx;

	while (childIdx = GetHiPriChildIDX(ph, parentIdx))
	{
		if (lastElem.pr <= ph->heapArr[childIdx].pr)
			break;
		ph->heapArr[parentIdx] = ph->heapArr[childIdx];
		parentIdx = childIdx;
	}

	ph->heapArr[parentIdx] = lastElem;
	ph->numOfData -= 1;
	return retData;
}
```

### 메인
```c
#include <stdio.h>
#include "SimpleHeap.h"

int main(void)
{
	Heap heap;
	HeapInit(&heap);

	HInsert(&heap, 'A', 1);
	HInsert(&heap, 'B', 1);
	HInsert(&heap, 'C', 1);
	printf("%c \n", HDelete(&heap));
	
	HInsert(&heap, 'A', 1);
	HInsert(&heap, 'B', 1);
	HInsert(&heap, 'C', 1);
	printf("%c \n", HDelete(&heap));

	while(!HIsEmpty(&heap))
		printf("%c \n", HDelete(&heap));

	return 0;
}
```

## 유용한 큐 & 우선순위 큐 구현
### 헤더(유용한 큐)
```c
#ifndef __USEFUL_HEAP_H__
#define __USEFUL_HEAP_H__

#define TRUE		1
#define FALSE		0

#define HEAP_LEN	100

typedef char HData;
typedef int (PriorityComp)(HData d1, HData d2);

typedef struct __heap
{
	PriorityComp* comp;
	int numOfData;
	HData heapArr[HEAP_LEN];
} Heap;

void HeapInit(Heap* ph, PriorityComp pc);
int HIsEmpty(Heap* ph);

void HInsert(Heap* ph, HData data);
HData HDelete(Heap* ph);


#endif
```

### 소스(유용한 큐)
```c
#include <stdio.h>
#include "UseFulHeap.h"

void HeapInit(Heap* ph, PriorityComp pc)
{
	ph->numOfData = 0;
	ph->comp = pc;
}

int HIsEmpty(Heap* ph)
{
	if (ph->numOfData == 0)
		return TRUE;
	else
		return FALSE;
}

int GetParentIdx(int idx)
{
	return idx / 2;
}

int GetLeftChildIdx(int idx)
{
	return idx * 2;
}

int GetRightChildIdx(int idx)
{
	return idx * 2 + 1;
}

int GetHiPriChildIdx(Heap* ph, int idx)
{
	if (GetLeftChildIdx(idx) > ph->numOfData)
		return 0;

	else if (GetLeftChildIdx(idx) == ph->numOfData)
		return GetLeftChildIdx(idx);

	else
	{
		if (ph->comp(ph->heapArr[GetLeftChildIdx(idx)], ph->heapArr[GetRightChildIdx(idx)]) >= 0)
			return GetRightChildIdx(idx);
		else
			return GetLeftChildIdx(idx);
	}
}

void HInsert(Heap* ph, HData data)
{
	int idx = ph->numOfData + 1;

	while (idx != 1)
	{
		if (ph->comp(data, ph->heapArr[GetParentIdx(idx)]) > 0)
		{
			ph->heapArr[idx] = ph->heapArr[GetParentIdx(idx)];
			idx = GetParentIdx(idx);
		}
		else
		{
			break;
		}
	}

	ph->heapArr[idx] = data;
	ph->numOfData++;
}

HData HDelete(Heap* ph)
{
	HData rdata = ph->heapArr[1];
	HData lastData = ph->heapArr[ph->numOfData];

	int parentIdx = 1;
	int childIndx;

	while (childIndx = GetHiPriChildIdx(ph, parentIdx))
	{
		if (ph->comp(lastData, ph->heapArr[childIndx]) >= 0)
			break;

		ph->heapArr[parentIdx] = ph->heapArr[childIndx];
		parentIdx = childIndx;
	}

	ph->heapArr[parentIdx] = lastData;
	ph->numOfData--;
	return rdata;
}
```

### 메인
```c
#include <stdio.h>
#include "UseFulHeap.h"

int DataPriComp(char ch1, char ch2)
{
	return ch2 - ch1;
}

int main(void)
{
	Heap heap;
	HeapInit(&heap, DataPriComp);

	HInsert(&heap, 'A');
	HInsert(&heap, 'B');
	HInsert(&heap, 'C');
	printf("%c \n", HDelete(&heap));


	HInsert(&heap, 'A');
	HInsert(&heap, 'B');
	HInsert(&heap, 'C');
	printf("%c \n", HDelete(&heap));

	while (!HIsEmpty(&heap))
		printf("%c \n", HDelete(&heap));

	return 0;
}
```

### 헤더(우선순위 큐)
```c
#ifndef __PRIORITY_QUEUE_H__
#define __PRIORITY_QUEUE_H_

#include "UseFulHeap.h"

typedef Heap PQueue;
typedef HData PQData;

void PQueueInit(PQueue* ppq, PriorityComp pc);

int PQIsEmpty(PQueue* ppq);

void PEnqueue(PQueue* ppq, PQData data);

PQData PDequeue(PQueue* ppq);

#endif
```

### 소스(우선순위 큐)
```c
#include <stdio.h>
#include "PriorityQueue.h"
#include "UseFulHeap.h"

void PQueueInit(PQueue* ppq, PriorityComp pc)
{
	HeapInit(ppq, pc);
}

int PQIsEmpty(PQueue* ppq)
{
	return HIsEmpty(ppq);
}

void PEnqueue(PQueue* ppq, PQData data)
{
	HInsert(ppq, data);
}

PQData PDequeue(PQueue* ppq)
{
	return HDelete(ppq);
}
```

### 메인
```c
#include <stdio.h>
#include "PriorityQueue.h"


int DataPriComp(char ch1, char ch2)
{
	return ch2 - ch1;
}

int main(void)
{
	PQueue pq;
	PQueueInit(&pq, DataPriComp);

	PEnqueue(&pq, 'A');
	PEnqueue(&pq, 'B');
	PEnqueue(&pq, 'C');
	printf("%c \n", PDequeue(&pq));

	PEnqueue(&pq, 'A');
	PEnqueue(&pq, 'B');
	PEnqueue(&pq, 'C');
	printf("%c \n", PDequeue(&pq));

	while(!PQIsEmpty(&pq))
		printf("%c \n", PDequeue(&pq));
}
```

# reference
윤성우의 열혈 자료구조 - 윤성우
