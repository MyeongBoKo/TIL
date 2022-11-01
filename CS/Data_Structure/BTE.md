## 후위 피법의 수식을 기반으로 수식 트리 구성
### 수식 트리의 구성을 위해서 후위 표기법의 특성
1. 연산 순서대로 왼쪽에서 오른쪽으로 연산자가 나열

2. 해당 연산자의 두 피연산자는 연산자 앞에 위치

즉, 후위 표기법의 수식에서 앞쪽에서 등장하는 피연산자와연산자를 이용해서 트리의 하단을 만들고, 이를 바탕으로 수식 트리의 윗부분을 구성해 나감.

### 수식 트리의 구성
1. 수식을 이루는 문자들을 처리할 때, 문자가 피연산자의 경우 스택으로 옮긴다.
2. 피연산자의 경우 스택으로 옮긴다.
3. 연산자가 등장하면, 스택에 쌓여있는 두 개의 피연산자를 꺼내서 연산자의 자식 노드로 연결한다. 이때 먼저 꺼내진 피연산자가 오른쪽 노드에 위치하고, 뒤에 나온 피연산자는 왼쪽 노드에 위치한다.
4. 구현된 수식 트리를 전부 스택에 옮긴다. 이 수식 트리 역시 다른 연산자의 자식 노드가 되기 때문이다.
   
5. 이렇게 스택에 쌓는 과정을 거친다.

<정리>
- 피연산자의 경우 무조건 스택으로 옮긴다.
- 연산자를 만나면 스택에서 두 개의 피연산자를 꺼내어 자식 노드로 연결한다.
- 자식 노드를 연결해서 만들어진 트리는 다시 스택으로 옮긴다.

### 수식 트리의 순회
- 전위 순회하여 데이터를 출력한 결과 - 전위 표기법의 수식
- 중위 순회하여 데이터를 출력한 결과 - 중위 표기법의 수식
- 후위 순회하여 데이터를 출력한 결과 - 후위 ㅍ기법의 수식

## 헤더
```c
#ifndef __EXPRESSION_TREE_H__
#define __EXPRESSION_TREE_H__

#include "BinaryTree2.h"

BTreeNode* MakeExpTree(char exp[]);			// 수식 트리 구성
int EvaluateExpTree(BTreeNode* bt);			// 수식 트리 계산

void ShowPrefixTypeExp(BTreeNode* bt);		// 전위 표기법 기반 출력	
void ShowInfixTypeExp(BTreeNode* bt);		// 후위 표기법 기반 출력
void ShowPostfixTypeExp(BTreeNode* bt);		// 후위 표기법 기반 출력

#endif
```

## 소스
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>
#include "ListBaseStack.h"
#include "BinaryTree2.h"

BTreeNode* MakeExpTree(char exp[])
{
	Stack stack;
	BTreeNode* pnode;

	int expLen = strlen(exp);
	int i;

	StackInit(&stack);

	for (i = 0; i < expLen; i++)
	{
		pnode = MakeBTreeNode();

		if (isdigit(exp[i]))
		{
			SetData(pnode, exp[i] - '0');
		}
		else
		{
			MakeRigthSubTree(pnode, SPop(&stack));
			MakeLeftSubTree(pnode, SPop(&stack));
			SetData(pnode, exp[i]);
		}

		SPush(&stack, pnode);
	}

	return SPop(&stack);
}

int EvaluateExpTree(BTreeNode* bt)
{
	int op1, op2;

	if (GetLeftSubTree(bt) == NULL && GetRightSubTree(bt) == NULL)
		return GetData(bt);

	op1 = EvaluateExpTree(GetLeftSubTree(bt));
	op2 = EvaluateExpTree(GetRightSubTree(bt));

	switch (GetData(bt))
	{
	case '+':
		return op1 + op2;
	case '-':
		return op1 - op2;
	case '*':
		return op1 * op2;
	case '/':
		return op1 / op2;
	}

	return 0;
}

void ShowNodeData(int data)
{
	if (0 <= data && data <= 9)
		printf("%d ", data);    // 피연산자의 출력
	else
		printf("%c ", data);    // 연산자의 출력
}

void ShowPrefixTypeExp(BTreeNode* bt)   // 전위 표기법으로 수식 출력
{
	PreorderTraverse(bt, ShowNodeData);
}

void ShowInfixTypeExp(BTreeNode* bt)    // 중위 표기법으로 수식 출력
{
	InorderTraverse(bt, ShowNodeData);
}

void ShowPostfixTypeExp(BTreeNode* bt)  // 후위 표기법으로 수식 출력
{
	PostorderTraverse(bt, ShowNodeData);
}
```

## 메인
```c
#include <stdio.h>
#include "ExpressionTree.h"

int main(void)
{
	char exp[] = "12+7*";
	BTreeNode* eTree = MakeBTreeNode(exp);

	printf("전위 표기법의 수식: ");
	ShowPrefixTypeExp(eTree);
	printf("\n");

	printf("중위 표기법의 수식: ");
	ShowInfixTypeExp(eTree);
	printf("\n");

	printf("후위 표기법의 수식: ");
	ShowPostfixTypeExp(eTree);
	printf("\n");

	printf("연산의 결과: %d \n", EvaluateExpTree(eTree));

	return 0;
}
```

# reference
윤성우의 열혈 자료구조 - 윤성우
