# ArrayList

## ArrayList.h
```c
#ifndef __ARRAY_LIST_H__
#define __ARRAY_LIST_H__

#include "Point.h"

#define TRUE		1
#define FALSE		0

#define LIST_LEN	100

typedef Point* LData;

typedef struct __ArrayList
{
	LData arr[LIST_LEN];
	int numOfData;
	int curPosition;
} ArrayList;

typedef ArrayList List;

void ListInit(List* plist);
void LInsert(List* plist, LData data);

int LFirst(List* plist, LData* pdata);
int LNext(List* plist, LData* pdata);

LData LRemove(List* plist);
int LCount(List* plist);

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
	if (plist->numOfData >= LIST_LEN) {
		puts("Error!");
		return;
	}

	plist->arr[plist->numOfData] = data;
	(plist->numOfData)++;
}

int LFirst(List* plist, LData* pdata)
{
	if (plist->numOfData == 0)
		return FALSE;

	(plist->curPosition) = 0;
	*pdata = plist->arr[0];
	return TRUE;
}

int LNext(List* plist, LData* pdata)
{
	if (plist->curPosition >= (plist->numOfData) - 1)
		return FALSE;

	(plist->curPosition)++;
	*pdata = plist->arr[plist->curPosition];
	return TRUE;
}

LData LRemove(List* plist)
{
	int rpos = plist->curPosition;
	LData rdata = plist->arr[rpos];
	int num = plist -> numOfData;
	int i;

	for (i = rpos;i< num - 1; i++)
		plist->arr[i] = plist->arr[i + 1];

	(plist->numOfData)--;
	(plist->curPosition)--;
	return rdata;
}

int LCount(List* plist) 
{
	return plist->numOfData;
}

```

## Point.h
```c
#ifndef __POINT_H__
#define __POINT_H__

typedef struct __point
{
	int xpos;		// x좌표를 저장
	int ypos;		// y좌표를 저장
} Point;

// 구조체 변수에 값을 저장하는 함수, Point 변수의 xpos, ypos 값 설정
void SetPointPos(Point* ppos, int xpos, int ypos);

// 저장된 값의 정보를 출력하는 함수, point 변수의 xpos, ypos 값 출력
void ShowPointPos(Point* ppos);

// 두 구조체 변수에 저장된 값을 비교하여 그 결과를 반환하는 함수, 두 Point 변수의 비교
int PointComp(Point* pos1, Point* pos2);

#endif
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
	printf("[%d, %d] ", ppos->xpos, ppos->ypos);
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

## 3-1예제
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

## 3-2 예제
```c
#ifndef __NAME_CARD_H__
#define __NAME_CARD_H__

#define TRUE		1
#define FALSE		0

#define NAME_LEN	30
#define PHONE_LEN	30

typedef struct __namecard
{
	char name[NAME_LEN];
	char phone[PHONE_LEN];
} NameCard;

NameCard* MakeNameCard(char* name, char* phone);

void ShowNameCardInfo(NameCard* pcard);

int NameCardCompare(NameCard* pcard, char* name);

void ChangePhoneNum(NameCard* pcard, char* phone);

#endif
```

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include "NameCard.h"

NameCard* MakeNameCard(char* name, char* phone)
{
	NameCard* newCard = (NameCard*)malloc(sizeof(NameCard));
	strycpy(newCard->name, name);
	strycpy(newCard->phone, phone);
	return newCard;
}

void ShowNameCardInfo(NameCard* pcard)
{
	printf("[이름] = %s \n", pcard->name);
	printf("[번호] = %s \n", pcard->phone);
}

int NameCardCompare(NameCard* pcard, char* name)
{
	return strcmp(pcard->name, name);
}

void ChangePhoneNum(NameCard* pcard, char* phone)
{
	strcpy(pcard->phone, phone);
}
```


# reference
윤성우의 열혈 자료구조 - 윤성우
