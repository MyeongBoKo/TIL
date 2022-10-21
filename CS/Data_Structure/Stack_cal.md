# 스택의 활용
## ListBaseStack.h
```c
#ifndef __LIST_BASE_STACK_H__
#define __LIST_BASE_STACK_H__

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
int SIsEmpty(Stack* pstack);

void SPush(Stack* pstack, Data data);
Data SPop(Stack* pstack);
Data SPeek(Stack* pstack);

#endif

```

## ListBaseStack.c
```c
#include <stdio.h>
#include <stdlib.h>
#include "ListBaseStack.h"

void StackInit(Stack* pstack)
{
	pstack->head = NULL;
}

int SIsEmpty(Stack* pstack)
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

	if (SIsEmpty(pstack)) {
		printf("Stack Memory Error!");
		exit(-1);
	}
	rdata = pstack->head->data;
	rnode = pstack->head;

	pstack->head = pstack->head->next;
	free(rnode);
	return rdata;
}

Data SPeek(Stack* pstack)
{
	if (SIsEmpty(pstack)) {
		printf("Stack Memory Error!");
		exit(-1);
	}

	return pstack->head->data;
}

```

# 후위 표기법의 수식으로 변환
## InfixToPostfix.h
```c
#ifndef __INFIX_TO_POSTIFIX_H__
#define __INFIX_TO_POSTIFIX_H__

void ConvToRPNExp(char exp[]);

#endif
```
## InfixToPostfix.c
```c
#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>
#include "ListBaseStack.h"

int GetOpPrec(char op)		// 연산자의 연산 우선순위 정보를 반환
{
	switch (op)
	{
	case '*':
	case '/':
		return 5;			// 가장 높은 연산의 우선순위
	case '+':
	case '-':
		return 3;
	case '(':
		return 1;			// 가장 낮은 연산의 우선순위
	}
	return -1;				// 등록하지 않은 연산자에 대한 값
}

int WhoPrecOp(char op1, char op2)
{
	int op1Prec = GetOpPrec(op1);
	int op2Prec = GetOpPrec(op2);

	if (op1Prec > op2Prec)			// op1의 우선순위가 더 높은 경우
		return 1;
	else if (op1Prec < op2Prec)		// op2의 우선순위가 더 높은 경우
		return -1;
	else
		return 0;					// op1, op2 우선순위가 같은 경우
}

void ConvToRPNExp(char exp[])
{
	Stack stack;
	int expLen = strlen(exp);
	char* convExp = (char*)malloc(expLen + 1);		// 변환된 수식을 담을 공간 마련

	int i, idx = 0;
	char tok, popOp;

	memset(convExp, 0, sizeof(char) * expLen + 1);
	StackInit(&stack);

	for (i = 0; i < expLen; i++)
	{
		tok = exp[i];		// exp로 전달된 수식을 한 문장씩 tok에 저장
		if (isdigit(tok))	// tok에 저장된 문자가 숫자의 경우 1을 반환
		{
			convExp[idx++] = tok;
		}
		else                // 연산자의 경우 
		{
			switch (tok)
			{
			case '(':
				SPush(&stack, tok);	// tok를 스택에 쌓는다.
				break;
			case ')':				// 닫는 소괄호를 만나면
				while (1)
				{
					popOp = SPop(&stack);	// 스택에서 연산자를 꺼내서
					if (popOp == '(')		// 연산자 ( 을 만날 때까지	
						break;
					convExp[idx++] = popOp;	// 배열 convExp에 저장
				}
				break;
			case '+': case '-':
			case '*': case '/':
				while (!SIsEmpty(&stack) && WhoPrecOp(SPeek(&stack), tok) >= 0)
					convExp[idx++] = SPop(&stack);
				SPush(&stack, tok);
				break;
			}
		}
	}
	while (!SIsEmpty(&stack))			// 스택에 남아 있는 모든 연산자들
		convExp[idx++] = SPop(&stack);	// 배열로 이동

	strcpy(exp, convExp);				// 변환된 수식을 exp에 복사
	free(convExp);						// convExp를 소멸
}
```

# 후위 표기법의 수식을 계산
## PostCalculator.h
```c
#ifndef __POST_CALCULATOR_H__
#define __POST_CALCULATOR_H__

int EvalRPNExp(char exp[]);

#endif
```
## PostCalculator.c
```c
#include <string.h>
#include <ctype.h>
#include "ListBaseStack.h"

int EvalRPNExp(char exp[])	// 후위표기법의 수식을 계산해서 결과 값을 반환
{
	Stack stack;
	int expLen = strlen(exp);
	int i;
	char tok, op1, op2;

	StackInit(&stack);

	for (i = 0; i < expLen; i++)
	{
		tok = exp[i];
		if (isdigit(tok))
		{
			SPush(&stack, tok - '0');
		}
		else
		{
			op2 = SPop(&stack);
			op1 = SPop(&stack);

			switch (tok)
			{
			case '+':
				SPush(&stack, op1 + op2);
				break;
			case '-':
				SPush(&stack, op1 - op2);
				break;
			case '*':
				SPush(&stack, op1 * op2);
				break;
			case '/':
				SPush(&stack, op1 / op2);
				break;
			}
		}
	}
	return SPop(&stack);	// 마지막 연산결과를 스택에서 꺼내어 반환

}
```

# 중위 표기법의 수식을 계산
## InfixCalculator.h
```c
#ifndef __INFIX_TO_POSTIFIX_H__
#define __INFIX_TO_POSTIFIX_H__

void ConvToRPNExp(char exp[]);

#endif
```
## InfixCalculator.c
```c
#define _CRT_SECURE_NO_WARNINGS
#include <string.h>
#include <stdlib.h>
#include "InfixToPostfix.h"		// convToRPNExp 함수의 호출
#include "PostCalculator.h"		// EvalRPNExp 함수의 호출

int EvalInfixExp(char exp)
{
	int len = strlen(exp);
	int ret;
	char* expcpy = (char*)malloc(len + 1);		// 문자열 저장공간 마련
	strcpy(expcpy, exp);						// exp를 expcpy에 복사

	ConvToRPNExp(expcpy);						// 후위 표기법의 수식으로 변환
	ret = EvalRPNExp(expcpy);					// 변환된 수식의 계산

	free(expcpy);								// 문자열 저장공간 해제
	return ret;									// 계산결과 반환
}
```

# main
```c
#include <stdio.h>
#include "InfixCalculator.h"

int main(void)
{
	char exp1[] = "1+2*3";

	printf("%s = %d", exp1, EvalInfixExp(exp1));
}
```

# 윤성우의 열혈 자료구조 - 윤성우
