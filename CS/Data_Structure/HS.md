# 힙 정렬

## 메인
```c
#include <stdio.h>
#include "UsefulHeap.h"

int PriComp(int n1, int n2)
{
	return n2 - n1;		// 오름차순 정렬을 위한 문장
}

void HeapSort(int arr[], int n, PriorityComp pc)
{
	Heap heap;
	int i;

	HeapInit(&heap, pc);

	for (i = 0; i < n; i++)	// 정렬대상을 가지고 힙을 구성
		HInsert(&heap, arr[i]);

	for (i = 0; i < n; i++)	// 순서대로 하나씩 꺼내서 정렬을 완성
		arr[i] = HDelete(&heap);
}

int main(void)
{
	int arr[4] = { 3, 4, 2, 1 };
	int i;

	HeapSort(arr, sizeof(arr) / sizeof(int), PriComp);

	for (i = 0; i < 4; i++)
		printf("%d ", arr[i]);

	printf("\n");
	return 0;
}
```
## 헤더
```c
#ifndef __USEFUL_HEAP_H__
#define __USEFUL_HEAP_H__

#define TRUE		1
#define FALSE		0

#define HEAP_LEN	100

typedef int HData;
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
## 소스
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

# reference
윤성우의 열혈 c 자료구조 - 윤성우



