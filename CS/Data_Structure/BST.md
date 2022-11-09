# 이진 탐색 트리
- 데이터를 저장하는 규칙 존재
- 이 규칙은 특정 데이터의 위치를 찾는데 사용

- <조건>
  - 이진 탐색 트리의 노드에 저장된 키(key)는 유일
  - 루트 노드의 키가 왼쪽 서브 트리를 구성하는 어떠한 노드보다 크다.
  - 루트 노드의 키가 오른쪽 서브 트리를 구성하는 어떠한 노드보다 작다.
  - 왼쪽과 오른쪽 서브 트리도 이진 탐색 트리
- 왼쪽 자식 노드의 키 < 부모 노드의 키 < 오른쪽 자식 노드의 키

- 탐색: 목표한 대상을 찾았다면 이를 저장하고 있는 노드의 주소 값이 반환, `BSTGetNodeData` 함수를 통해 노드에 저장된 값을 얻을 수 있다.

## BinaryTree2.h
```c
#ifndef __BINARY_TREE2_H__
#define __BINARY_TREE2_H__

typedef int BTData;

typedef struct __bTreeNode
{
	BTData data;
	struct __bTreeNode* left;
	struct __bTreeNode* right;
} BTreeNode;

BTreeNode* MakeBTreeNode(void);
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

#endif

```
## BinaryTree2.c
```c
#include <stdio.h>
#include <stdlib.h>
#include "BinaryTree2.h"

BTreeNode* MakeBTreeNode(void)
{
	BTreeNode* nd = (BTreeNode*)malloc(sizeof(BTreeNode));
	nd->left = NULL;
	nd->right = NULL;
	return nd;
}

BTData GetData(BTreeNode* bt)
{
	return bt->data;
}

void SetData(BTreeNode* bt, BTData data)
{
	bt->data = data;
}

BTreeNode* GetLeftSubTree(BTreeNode* bt)
{
	return bt->left;
}

BTreeNode* GetRightSubTree(BTreeNode* bt)
{
	return bt->right;
}

void MakeLeftSubTree(BTreeNode* main, BTreeNode* sub)
{
	if (main->left != NULL)
		free(main->left);

	main->left = sub;
}

void MakeRightSubTree(BTreeNode* main, BTreeNode* sub)
{
	if (main->right != NULL)
		free(main->right);

	main->right = sub;
}

void PreorderTraverse(BTreeNode* bt, VisitFunPtr action)
{
	if (bt == NULL)
		return;

	action(bt->data);
	PreorderTraverse(bt->left, action);
	PreorderTraverse(bt->right, action);
}

void InorderTraverse(BTreeNode* bt, VisitFunPtr action)
{
	if (bt == NULL)
		return;

	InorderTraverse(bt->left, action);
	action(bt->data);
	InorderTraverse(bt->right, action);
}

void PostorderTraverse(BTreeNode* bt, VisitFunPtr action)
{
	if (bt == NULL)
		return;

	PostorderTraverse(bt->left, action);
	PostorderTraverse(bt->right, action);
	action(bt->data);
}
```
## BinarySerachTree.h
```c
#ifndef __BINARY_SEARCH_TREE_H__
#define __BINARY_SEARCH_TREE_H__

#include "BinaryTree2.h"

typedef BTData BSTData;

// BST의 생성 및 초기화
void BSTMakeAndInit(BTreeNode** pRoot);

// 노드에 저장된 데이터 반환
BSTData BSTGetNodeData(BTreeNode* bst);

// BST를 대상으로 데이터 저장(노드의 생성과정 포함)
void BSTInsert(BTreeNode**pRoot, BSTData data);

// BST를 대상으로 데이터 탐색
BTreeNode* BSTSearch(BTreeNode* bst, BSTData target);

#endif
```
## BinarySearchTree.c
```c
#include <stdio.h>
#include <stdlib.h>
#include "BinarySearchTree.h"

void BSTMakeAndInit(BTreeNode** pRoot)
{
	*pRoot = NULL;
}

BSTData BSTGetNodeData(BTreeNode* bst)
{
	return GetData(bst);
}

void BSTInsert(BTreeNode** pRoot, BSTData data)
{
	BTreeNode* pNode = NULL;	// parent Node
	BTreeNode* cNode = *pRoot;	// curent Node
	BTreeNode* nNode = NULL;	// new Node

	// 새로운 노드가 추가될 위치를 찾는다.
	while (cNode != NULL)	// cNode가 NULL이 아니면 반복
	{
		if (data == GetData(cNode))
			return;			// 데이터(키)의 중복 허용 X

		pNode = cNode;		

		if (GetData(cNode) > data)
			cNode = GetLeftSubTree(cNode);	// cNode는 현재 노드의 왼쪽 노드의 주소값을 받음
		else
			cNode = GetRightSubTree(cNode);	// cNode는 현재 노드의 오른쪽 노드의 주소값을 받음
	}

	// pNode의 자식 노드로 추가할 새 노드의 생성
	nNode = MakeBTreeNode();				// 새 노드의 생성
	SetData(nNode, data);					// 새 노드에 데이터 저장

	// pNode의 자식 노드로 새 노드를 추가
	if (pNode != NULL)						// 새 노드가 루트 노드가 아니면
	{
		if (data < GetData(pNode))
			MakeLeftSubTree(pNode, nNode);
		else
			MakeRightSubTree(pNode, nNode);
	}
	else                                    // 새 노드가 루트 노드라면
	{
		*pRoot = nNode;						// 새 노드를 루트 노드로 지정
	}
}

BTreeNode* BSTSearch(BTreeNode* bst, BSTData target)
{
	BTreeNode* cNode = bst;					// cNode에 bst 주소값 저장
	BSTData cd;

	while (cNode != NULL)
	{
		cd = GetData(cNode);

		if (target == cd)
			return cNode;
		else if (target < cd)
			cNode = GetLeftSubTree(cNode);	// cNode는 cNode의 왼쪽 노드 주소 값
		else
			cNode = GetRightSubTree(cNode);	// cNode는 cNode의 오른쪽 노드 주소 값
	}

	return NULL;
}
```

# reference 
윤성우의 열혈 C 자료구조 - 윤성우
