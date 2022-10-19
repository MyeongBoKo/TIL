# 스택
- 나중에 들어간 것이 먼저 나오는 구조
- LIFO(Last-In, First-Out)

# 배열 기반의 스택 구현
## 헤더파일
```c
#ifndef __ARRAYBASE_STACK_H__
#define __ARRAYBASE_STACK_H__

#define TRUE		1
#define FALSE		0
#define STACK_LEN	100

typedef int Data;

typedef struct __arrayStack
{
	Data stackArr[STACK_LEN];			// typedef int Data;	
	int topIndex;
} ArrayStack;

typedef ArrayStack Stack;

void StackInit(Stack* pstack);			// 스택의 초기화
int SIsEmpty(Stack* pstack);			// 스택이 비어있는지 확인

void SPush(Stack* pstack, Data data);	// 스택의 push 연산
Data SPop(Stack* pstack);				// 스택의 pop 연산
Data SPeek(Stack* pstack);				// 스택의 peek 연산

#endif
```

## 소스파일
```c
#include <stdio.h>
#include <stdlib.h>
#include "ArrayBaseStack.h"

void StackInit(Stack* pstack)
{
	pstack->topIndex = -1;		// topIndex가 -1이면 빈 상태를 의미
}

int SIsEmpty(Stack* pstack)
{
	if (pstack->topIndex == -1)
		return TRUE;
	else
		return FALSE;
}

void SPush(Stack* pstack, Data data)
{
	pstack->topIndex += 1;
	pstack->stackArr[pstack->topIndex] = data;
}

Data SPop(Stack* pstack)
{
	int rIdx;

	if (SIsEmpty(pstack)) {
		printf("Stack Memory Error!");
		exit(-1);
	}

	rIdx = pstack->topIndex;
	pstack->topIndex -= 1;

	return pstack->stackArr[rIdx];
}

Data SPeek(Stack* pstack)
{
	if (SIsEmpty(pstack)) {
		printf("Stack Memory Eror!");
		exit(-1);
	}

	return pstack->stackArr[pstack->topIndex];
}
```

## 메인
```c
#include <stdio.h>
#include "ArrayBaseStack.h"

int main(void)
{
	Stack stack;
	StackInit(&stack);

	SPush(&stack, 1);	SPush(&stack, 2);	SPush(&stack, 3);
	SPush(&stack, 4);	SPush(&stack, 5);	SPush(&stack, 6);

	while (!SIsEmpty(&stack)) {
		printf("%d ", SPop(&stack));
	}

	return 0;
}
```


# 연결 리스트 기반의 스택 구현
## 헤더파일
```c
#ifndef __LISTBASE_STACK_H__
#define __LISTBASE_STACK_H__

#define TRUE		1
#define FALSE		0

typedef int Data;

typedef struct __node
{
	Data data;
	struct __node* next;
} Node;

typedef struct __listStack
{
	Node* head;
} ListStack;

typedef ListStack Stack;

void StackInit(Stack* pstack);
int SIsempty(Stack* pstack);

void SPush(Stack* pstack, Data data);
Data SPop(Stack* pstack);
Data Speek(Stack* pstack);

#endif
```

## 소스파일
```c
#include <stdio.h>
#include <stdlib.h>
#include "ListBaseStack.h"

void StackInit(Stack* pstack)
{
	pstack->head == NULL;
}

int SIsempty(Stack* pstack)
{
	if (pstack->head == NULL)
		return TRUE;
	else
		return FALSE;
}

void SPush(Stack* pstack, Data data)
{
	Node* newNode = (Node*)malloc(sizeof(Node));
	
	newNode->data = data;
    newNode->next = pstack->head;
	pstack->head = newNode;
}

Data SPop(Stack* pstack)
{
	Data rdata;
	Node* rnode;

	if (SIsempty(pstack)) {
		printf("Stack Memory Error!");
		exit(-1);
	}
	
	rdata = pstack->head->data;
	rnode = pstack->head;

	pstack->head = pstack->head->next;
	free(rnode);
	
	return rdata;
}

Data Speek(Stack* pstack)
{
	if (SIsempty(pstack)) {
		printf("Stack Memory Error!");
		exit(-1);
	}
	return pstack->head->data;
}
```

## 메인
```c
#include <stdio.h>
#include "ListBaseStack.h"

int main(void)
{
	Stack stack;
	StackInit(&stack);

	SPush(&stack, 6);	SPush(&stack, 5);
	SPush(&stack, 4);	SPush(&stack, 3);
	SPush(&stack, 2);	SPush(&stack, 1);

	printf("\n%d \n", Speek(&stack));

	while (!SIsempty(&stack)) {
		printf("%d ", SPop(&stack));
	}
	return 0;
}
```

# reference
윤성우의 열혈 자료구조 - 윤성우
