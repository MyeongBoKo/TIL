# 균형 잡힌 이진 탐색 트리(AVL)
- 이진 탐색 트리는 저장 순서에 따라 탐색의 성능에 큰 차이를 보이는 단점

- 이진 탐색 트리의 단점을 해결한 트리의 종류 중 하나인 AVL
- AVL은 트리에 노드가 추가될 때, 삭제될 때 트리의 균형상태를 파악해서 스스로 구조를 변경하여 균형을 잡는 트리다.
- 균형의 정도를 표현하기 위해 균형 인수를 사용한다.
- 균형 인수(Balance Factor)란 왼쪽 서브 트리의 높이 - 오른쪽 서브 트리의 높이
- 균형 인수를 통해서 리밸런싱(균형을 잡기 위한 트리 구조의 재조정)한다.

## LL회전
- 자식 노드 2개가 왼쪽으로 연이어 연결되어 있으면 균형 인수가 +2로 계산된다.

- 균형 인수가 +2로 계산된 상태를 `LL상태`라고 한다.
- LL상태에서 발생한 불균형의 해소를 위해 등장한 리밸런싱 방법을 `LL회전`이라고 한다.
- LL회전은 균형 인수가 +2인 노드를 균형 인수가 +1인 노드의 오른쪽 자식 노드가 되게 한다.
- 1)`ChnageLeftSubTree(pNode, GetRightSubTree(cNode))` 
- 2)`ChangeRightSubTree(cNode, pNode)`

## RR회전
- 자식 노드 2개가 오른쪽으로 연이어 연결되어 있으면 균형 인수가 -2로 계산된다

- 이때, 균형 인수가 -2로 계산된 상태를 `RR상태`라고 한다.
- RR상태에서 발생한 불균형의 해소를 위해 등장한 리밸런싱 방법을 `RR회전`이라고 한다.
- 1)`ChangeRightSubTree(pNode, GetLeftSubTree(cNode))`
- 2)`ChangeLeftSubTree(cNode, pNode)`

## LR회전
- 자식 노드가 왼쪽에 하나, 그리고 이어서 오른쪽에 하나 달린 상태를 `LR상태`라고 한다.

- `LR회전`은 부분적으로 RR회전에 이어서 LL회전을 진행한다.
- 루트 노드에 5가 저장, 왼쪽 자식 노드에 1이 저장, 왼쪽 자식 노드의 오른쪽 자식 노드에 3이 저장되었다고 가정
- 1)`RotateRR`함수를 호출해서 1이 저장된 노드를 중심으로 RR회전을 진행시킨다.
- 2)3이 저장된 노드의 주소 값이 반환된다.
- 3)`ChangeLeftSubTree`함수를 통해서 LL상태를 만든다.
- 4)`RotateLL`함수를 호출해서 LL회전을 시킨다.

## RL회전
- 자식 노드가 오른쪽에 하나, 그리고 이어서 왼쪽에 하나 달린 상태를 `RL상태`라고 한다.

- `RL회전`은 부분적으로 LL회전에 이어서 RR회전을 진행한다.
- 루트 노드에 5가 저장, 오른쪽 자식 노드에 1이 저장, 오른쪽 자식 노드의 왼쪽 자식 노드에 3이 저장되었다고 가정
- 1)`RotateLL`함수를 호출해서 1이 저장된 노드를 중심으로 LL회전을 진행시킨다.
- 2)3이 저장된 노드의 주소 값이 반환된다.
- 3)`ChangeRightSubTree`함수를 통해서 RR상태를 만든다.
- 4)`RotateRR`함수를 호출해서 RR회전을 시킨다.

## BinaryTree3.h
```c
#ifndef __BINARY_TREE3_H__
#define __BINARY_TREE3_H__

typedef int BTData;

typedef struct __bTreeNode
{
	BTData data;
	struct __bTreeNode* left;
	struct __bTreeNode* right;
} BTreeNode;

BTreeNode* makeBTreeNode(void);
BTData GetData(BTreeNode* bt);
void SetData(BTreeNode* bt, BTData data);

BTreeNode* GetLeftSubTree(BTreeNode* bt);
BTreeNode* GetRightSubTree(BTreeNode* bt);

void MakeLeftSubTree(BTreeNode* main, BTreeNode* sub);
void MakeRightSubTree(BTreeNode* main, BTreeNode* sub);

typedef void (*VisitFunPtr)(BTData data);

void PreorderTraverse(BTreeNode* bt, VisitFunPtr action);
void InorderTraverse(BTreeNode* bt, VisitFunPtr action);
void PostorderTraverse(BTreeNode* bt, VisitFunPtr action);

BTreeNode* RemoveLeftSubTree(BTreeNode* bt);
BTreeNode* RemoveRightSubTree(BTreeNode* bt);

void ChangeLeftSubTree(BTreeNode* main, BTreeNode* sub);
void ChangeRightSubTree(BTreeNode* main, BTreeNode* sub);

#endif
```

## BinaryTree3.c
```c
#include <stdio.h>
#include <stdlib.h>
#include "BinaryTree3.h"

BTreeNode* MakeBTreeNode(void)
{
	BTreeNode* node = (BTreeNode*)malloc(sizeof(BTreeNode));
	node->left = NULL;
	node->right = NULL;
	return node;
}

BTData GetData(BTreeNode* bt) {
	return bt->data;
}

void SetData(BTreeNode* bt, BTData data) {
	bt->data = data;
}

BTreeNode* GetLeftSubTree(BTreeNode* bt) {
	return bt->left;
}

BTreeNode* GetRightSubTree(BTreeNode* bt) {
	return bt->right;
}

void MakeLeftSubTree(BTreeNode* main, BTreeNode* sub) {
	if (main->left != NULL)
		free(main->left);

	main->left = sub;
}

void MakeRightSubTree(BTreeNode* main, BTreeNode* sub) {
	if (main->right != NULL)
		free(main->right);

	main->right = sub;
}

void PreorderTraverse(BTreeNode* bt, VisitFunPtr action) {
	if (bt == NULL)
		return;
	
	action(bt->data);
	PreorderTraverse(bt->left, action);
	PreorderTraverse(bt->right, action);
}

void InorderTraverse(BTreeNode* bt, VisitFunPtr action) {
	if (bt == NULL)
		return;

	InorderTraverse(bt->left, action);
	action(bt->data);
	InorderTraverse(bt->right, action);
}

void PostorderTraverse(BTreeNode* bt, VisitFunPtr action) {
	if (bt == NULL)
		return;

	PostorderTraverse(bt->left, action);
	PostorderTraverse(bt->right, action);
	action(bt->data);
}

BTreeNode* RemoveLeftSubTree(BTreeNode* bt) {
	BTreeNode* delNode;

	if (bt != NULL) {
		delNode = bt->left;
		bt->left = NULL;
	}
	return delNode;
}

BTreeNode* RemoveRightSubTree(BTreeNode* bt) {
	BTreeNode* delNode;

	if (bt != NULL) {
		delNode = bt->right;
		bt->right = NULL;
	}
	return delNode;
}

void ChangeLeftSubTree(BTreeNode* main, BTreeNode* sub) {
	main->left = sub;
}

void ChangeRightSubTree(BTreeNode* main, BTreeNode* sub) {
	main->right = sub;
}
```

## BinarySearchTree3.h
```c
#ifndef __BINARY_SEARCH_TREE3__
#define __BINARY_SEARCH_TREE3__

#include "BinaryTree3.h"

typedef BTData BSTData;

void BSTMakeAndInit(BTreeNode** pRoot);

BSTData BSTGetNodeData(BTreeNode* bt);

BTreeNode* removeBST(BTreeNode** pRoot, BSTData target);

BTreeNode* BSTSearch(BTreeNode* bst, BSTData target);

BTreeNode* BSTRemove(BTreeNode** pRoot, BSTData target);

void BSTShowAll(BTreeNode* bst);

#endif
```

## BinarySearchTree3.c
```c
#include <stdio.h>
#include <stdlib.h>
#include "BinarySearchTree3.h"
#include "AVLRebalance.h"

void BSTMakeAndInit(BTreeNode** pRoot)
{
	*pRoot = NULL;
}

BSTData BSTGetNodeData(BTreeNode* bst)
{
	return GetData(bst);
}

BTreeNode* BSTInsert(BTreeNode** pRoot, BSTData data)
{
	if (*pRoot == NULL)
	{
		*pRoot = MakeBTreeNode();
		SetData(*pRoot, data);
	}
	else if (data < GetData(*pRoot))
	{
		BSTInsert(&((*pRoot)->left), data);
		*pRoot = Rebalance(pRoot);
	}
	else if (data > GetData(*pRoot))
	{
		BSTInsert(&((*pRoot)->right), data);
		*pRoot = Rebalance(pRoot);
	}
	else
	{
		return NULL;
	}
	return *pRoot;
}

BTreeNode* BSTSearch(BTreeNode* bst, BSTData target)
{
	BTreeNode* cNode = bst;
	BSTData cd;

	while (cNode != NULL)
	{
		cd = GetData(cNode);

		if (target == cd)
			return cNode;
		else if (target < cd)
			cNode = GetLeftSubTree(cNode);
		else
			cNode = GetRightSubTree(cNode);
	}

	return NULL;
}

BTreeNode* BSTRemove(BTreeNode** pRoot, BSTData target)
{
	BTreeNode* pVRoot = MakeBTreeNode();
	BTreeNode* pNode = pVRoot;
	BTreeNode* cNode = *pRoot;
	BTreeNode* dNode;

	ChangeRightSubTree(pVRoot, *pRoot);

	while (cNode != NULL && GetData(cNode) != target)
	{
		pNode = cNode;

		if (target < GetData(cNode))
			cNode = GetLeftSubTree(cNode);
		else
			cNode = GetRightSubTree(cNode);
	}

	if (cNode == NULL)
		return NULL;

	dNode = cNode;

	if (GetLeftSubTree(dNode) == NULL && GetRightSubTree(dNode) == NULL)
	{
		if (GetLeftSubTree(pNode) == dNode)
			RemoveLeftSubTree(pNode);
		else
			RemoveRightSubTree(pNode);
	}

	else if (GetLeftSubTree(dNode) == NULL || GetRightSubTree(dNode) == NULL)
	{
		BTreeNode* dcNode;

		if (GetLeftSubTree(dNode) != NULL)
			dcNode = GetLeftSubTree(dNode);
		else
			dcNode = GetRightSubTree(dNode);

		if (GetLeftSubTree(pNode) == dNode)
			ChangeLeftSubTree(pNode, dcNode);
		else
			ChangeRightSubTree(pNode, dcNode);
	}

	else
	{
		BTreeNode* mNode = GetRightSubTree(dNode);
		BTreeNode* mpNode = dNode;
		int delData;

		while (GetLeftSubTree(mNode) != NULL)
		{
			mpNode = mNode;
			mNode = GetLeftSubTree(mNode);
		}

		delData = GetData(dNode);
		SetData(dNode, GetData(mNode));

		if (GetLeftSubTree(mpNode) == mNode)
			ChangeLeftSubTree(mpNode, GetRightSubTree(mNode));
		else
			ChangeRightSubTree(mpNode, GetRightSubTree(mNode));

		dNode = mNode;
		SetData(dNode, delData);
	}

	if (GetRightSubTree(pVRoot) != *pRoot)
		*pRoot = GetRightSubTree(pVRoot);

	free(pVRoot);
	*pRoot = Rebalance(pRoot);
	return dNode;
}
```

## AVLRebalance.h
```c
#ifndef __AVL_REBALANCE_H__
#define __AVL_REBALANCE_H__

#include "BinaryTree3.h"

// 트리의 균형을 잡는다.
BTreeNode* Rebalance(BTreeNode** pRoot);

#endif
```

## AVLRebalance.c
```c
#include <stdio.h>
#include "BinaryTree3.h"

//LL
BTreeNode* RotateLL(BTreeNode* bst)
{
	BTreeNode* pNode;	// parent node
	BTreeNode* cNode;	// curent node

	pNode = bst;
	cNode = GetLeftSubTree(pNode);

	ChangeLeftSubTree(pNode, GetRightSubTree(cNode));
	ChangeRightSubTree(cNode, pNode);

	return cNode;
}

// RR
BTreeNode* RotateRR(BTreeNode* bst)
{
	BTreeNode* pNode;
	BTreeNode* cNode;

	pNode = bst;
	cNode = GetRightSubTree(pNode);

	ChangeRightSubTree(pNode, GetLeftSubTree(cNode));
	ChangeLeftSubTree(cNode, pNode);

	return cNode;
}

// RL
BTreeNode* RotateRL(BTreeNode* bst)
{
	BTreeNode* pNode;
	BTreeNode* cNode;

	pNode = bst;
	cNode = GetRightSubTree(pNode);

	ChangeRightSubTree(pNode, RotateLL(cNode));
	return RotateRR(pNode);
}

// LR
BTreeNode* RotateLR(BTreeNode* bst)
{
	BTreeNode* pNode;
	BTreeNode* cNode;

	pNode = bst;
	cNode = GetLeftSubTree(pNode);

	ChangeLeftSubTree(pNode, RotateRR(cNode));
	return RotateLL(pNode);
}

// 트리의 높이를 계산해서 반환
int GetHeight(BTreeNode* bst)
{
	int leftH;
	int rightH;

	if (bst == NULL)
		return 0;

	leftH = GetHeight(GetLeftSubTree(bst));
	rightH = GetHeight(GetRightSubTree(bst));

	if (leftH > rightH)
		return leftH + 1;
	else
		return rightH + 1;
}


// 두 서브 트리의 높이의 차를 반환
int GetHeighDiff(BTreeNode* bst)
{
	int lsh;
	int rsh;

	if (bst == NULL)
		return 0;

	lsh = GetHeight(GetLeftSubTree(bst));
	rsh = GetHeight(GetRightSubTree(bst));
	return lsh - rsh;
}

// 트리의 균형을 잡는다.
BTreeNode* Rebalance(BTreeNode** pRoot)
{
	int hDiff = GetHeightDiff(*pRoot);

	if (hDiff > 1)
	{
		if (GetHeightDiff(GetLeftSubTree(*pRoot)) > 0)
			*pRoot = RotateLL(*pRoot);
		else
			*pRoot = RotateLR(*pRoot);
	}

	if (hDiff < -1)
	{
		if (GetHeighDiff(GetRightSubTree(*pRoot)) < -1)
			*pRoot = RotateRR(*pRoot);
		else
			*pRoot = RotateRL(*pRoot);
	}
	return *pRoot;
}
```

## main
```c
#include <stdio.h>
#include "BinaryTree3.h"
#include "BinarySearchTree3.h"

int main(void)
{
	BTreeNode* avlRoot;
	BTreeNode* clNode;
	BTreeNode* crNode;
	BSTMakeAndInit(&avlRoot);

	BSTInsert(&avlRoot, 1);
	BSTInsert(&avlRoot, 2);
	BSTInsert(&avlRoot, 3);
	BSTInsert(&avlRoot, 4);
	BSTInsert(&avlRoot, 5);
	BSTInsert(&avlRoot, 6);
	BSTInsert(&avlRoot, 7);
	BSTInsert(&avlRoot, 8);
	BSTInsert(&avlRoot, 9);

	printf("루트 노드: %d \n", GetData(avlRoot));

	clNode = GetLeftSubTree(avlRoot);
	crNode = GetRightSubTree(avlRoot);
	printf("왼쪽1: %d, 오른쪽1: %d \n", GetData(clNode), GetData(crNode));

	clNode = GetLeftSubTree(clNode);
	crNode = GetRightSubTree(crNode);
	printf("왼쪽2: %d, 오른쪽2: %d \n", GetData(clNode), GetData(crNode));

	clNode = GetLeftSubTree(clNode);
	crNode = GetRightSubTree(crNode);
	printf("왼쪽3: %d, 오른쪽3: %d \n", GetData(clNode), GetData(crNode));

	clNode = GetLeftSubTree(clNode);
	crNode = GetRightSubTree(crNode);
	printf("왼쪽4: %d, 오른쪽4: %d \n", GetData(clNode), GetData(crNode));
}
```

# reference
윤성우의 열혈 C자료구조 - 윤성우
