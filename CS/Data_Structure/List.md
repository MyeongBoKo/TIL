# 3-1예제
```c
#include <stdio.h>
#include "ArrayList.h"

int main(void)
{
	List list;
	int data;
	ListInit(&list);


	LInsert(&list, 1); LInsert(&list, 2); LInsert(&list, 3);
	LInsert(&list, 4); LInsert(&list, 5); LInsert(&list, 6);
	LInsert(&list, 7); LInsert(&list, 8); LInsert(&list, 9);

	
	if (LFirst(&list, &data))
	{
		int sum = 0;
		sum = sum + data;

		while (LNext(&list, &data))
			sum = sum + data;

		printf("데이터의 총 합: %d \n", sum);
	}
	
	if (LFirst(&list, &data))
	{
		if (data % 2 == 0 || data % 3 == 0)
			LRemove(&list);

		while (LNext(&list, &data))
		{
			if (data % 2 == 0 || data % 3 == 0)
				LRemove(&list);
		}
	}

	if (LFirst(&list, &data))
	{
		printf("데이터의 수: %d ", data);

		while (LNext(&list, &data))
			printf("%d ", data);
	}

	return 0;
}
```

## ArrayList.h
```c
#pragma once
#ifndef __ARRAY_LIST_H__
#define __ARRAY_LIST_H__

#define TRUE	1	// '참'을 표현하기 위한 매크로 정의
#define FALSE	0	// '거직'을 표현하기 위한 매크로 정의

#define LIST_LEN	100
typedef int LData;	// LData에 대한 typdef 선어

typedef struct __ArrayList	// 배열기반 리스트를 정의한 구조체
{
	LData arr[LIST_LEN];	// 리스트의 저장소인 배열
	int numOfData;			// 저장된 데이터 수
	int curPosition;		// 데이터 참조위치를 기록
} ArrayList;

typedef __ArrayList List;

void ListInit(List* plist);					// 초기화
void ListInsert(List* plist, LData data);	// 데이터 저장

void LFirst(List* plist, LData* pdata);		// 첫 데이터 참조
void LNext(List* plist, LData* pdata);		// 다음 데이터 참조

LData Remove(List* plist);					// 참조한 데이터 삭제
int LCount(List* plist);					// 저장된 데이터의 수 반환

#endif


```

## ArrayList.c
```c
#include <stdio.h>
#include "ArrayList.h"

void ListInit(List* plist)
{
	(plist->numOfData) = 0;
	(plist->curPosition) = -1;
}

void LInsert(List* plist, LData data)
{
	if (plist->numOfData >= LIST_LEN)
	{
		puts("저장이 불가합니다.");
		return;
	}

	(plist->arr[plist->numOfData]) = data;	// 데이터 증가
	
	(plist->numOfData)++;	// 저장된 데이터 수 증가
}

void LFirst(List* plist, LData* pdata)
{
	if (plist->numOfData == 0)
		return FALSE;

	(plist->curPosition) = 0;
	*pdata = plist->arr[0];
	return TRUE;
}

void LNext(List* plist, LData* pdata)
{
	if (plist->curPosition >= (plist->numOfData) - 1)
		return FALSE;

	(plist->curPosition)++;

	*pdata = plist->arr[plist->curPosition];
	return TRUE;
}

LData Remove(List* plist)
{
	int rpos = plist->curPosition;	// 삭제할 데이터의 인덱스 값 참조
	int num = plist->numOfData;
	int i;
	LData rdata = plist->arr[rpos];	// 삭제할 데이터 임시 보관

	for (i = rpos; i < num - 1; i++)
		plist->arr[i] = plist->arr[i + 1];

	(plist->numOfData)--;			// 데이터 수 감수
	(plist->curPosition)--;			// 참조위치를 하나 되돌린다.
	return rdata;					// 삭제된 데이터의 반환
}

int LCount(List* plist)
{
	return plist->numOfData;
}
```

## Point.c
```c
#include <stdio.h>
#include "Point.h"

void SetPointPos(Point* ppos, int xpos, int ypos)
{
	ppos->xpos = xpos;
	ppos->ypos = ypos;
}

void ShowPointPos(Point* ppos)
{
	printf("[%d, %d] \n", ppos -> xpos, ppos -> ypos);
}

int PointComp(Point* pos1, Point* pos2)
{
	if (pos1->xpos == pos2->xpos && pos1->ypos == pos2->ypos)
		return 0;
	else if (pos1->xpos == pos2->xpos)
		return 1;
	else if (pos1->ypos == pos2->ypos)
		return 2;
	else
		return -1;
}
```
## Point.h
```c
#pragma once
#ifndef __POINT_H__
#define __POINT_H__

typedef struct __point
{
	int xpos;	// x좌표 정보
	int ypos;	// y좌표 정보
} Point;

// Point 변수의 xpos, ypos 값 설정
void SetPointPos(Point* ppos, int xpos, int ypos);

// Point 변수의 xpos, ypos 정보 출력
void ShowPointPos(Point* ppos);

// 두 Point 변수의 비교
int PointComp(Point *pos1, Point *pos2)

#endif 
```

## main
```c
#include <stdio.h>
#include <stdlib.h>
#include "ArrayList.h"
#include "Point.h"

int main(void)
{
	List list;
	Point compPos;
	Point* ppos;

	ListInit(&list);

	// 4개의 데이터 저장
	ppos = (Point*)malloc(sizeof(Point));
	SetPointPos(ppos, 2, 1);
	LInsert(&list, ppos);

	ppos = (Point*)malloc(sizeof(Point));
	SetPointPos(ppos, 2, 2);
	LInsert(&list, ppos);

	ppos = (Point*)malloc(sizeof(Point));
	SetPointPos(ppos, 3, 1);
	LInsert(&list, ppos);

	ppos = (Point*)malloc(sizeof(Point));
	SetPointPos(ppos, 3, 2);
	LInsert(&list, ppos);

	// 저장된 데이터의 출력
	printf("현재 데이터의 수: %d \n", LCount(&list));

	if (LFirst(&list, &ppos))
	{
		ShowPointPos(ppos);

		while (LNext(&list, &ppos))
			ShowPointPos(ppos);
	}

	printf("\n");

	// xpos가 2인 모든 데이터 삭제
	compPos.xpos = 2;
	compPos.ypos = 0;

	if (LFirst(&list, &ppos))
	{
		if (PointComp(ppos, &compPos) == 1)
		{
			ppos = LRemove(&list);
			free(ppos);
		}

		while (LNext(&list, &ppos))
		{
			if (PointComp(ppos, &compPos) == 1)
			{
				ppos = LRemove(&list);
				free(ppos);
			}
		}
	}

	// 삭제 후 남은 데이터 전체 출력
	printf("현재 데이터의 수: %d \n", LCount(&list));

	if (LFirst(&list, &ppos))
	{
		ShowPointPos(ppos);

		while (LNext(&list, &ppos))
			ShowPointPos(ppos);
	}
	printf("\n");

	return 0;
}
```


# reference
윤성우의 열혈 자료구조 - 윤성우
