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

## BinaryTree3.h
```c
BTreeNode* RemoveLeftSubTree(BTreeNode* bt);
BTreeNode* RemoveRightSubTree(BTreeNode* bt);

void ChangeLeftSubTree(BTreeNode* main, BTreeNode* sub);
void ChangeRightSubTree(BTreeNode* main, BTreeNode* sub);
```

## BinaryTree3.c
```c
...

BTreeNode* RemoveLeftSubTree(BTreeNode* bt)
{
	BTreeNode* delNode;

	if (bt != NULL)
	{
		delNode = bt->left;
		bt->left = NULL;
	}
	return delNode;
}

BTreeNode* RemoveRightSubTree(BTreeNode* bt)
{
	BTreeNode* delNode;

	if (bt != NULL)
	{
		delNode = bt->right;
		bt->right = NULL;
	}
	return delNode;
}

void ChangeLeftSubTree(BTreeNode* main, BTreeNode* sub)
{
	main->left = sub;
}

void ChangeRightSubTree(BTreeNode* main, BTreeNode* sub)
{
	main->right = sub;
}
	
```

## BinarySearchTree2.h
```c
#ifndef __BINARY_SEARCH_H__
#define __BINARY_SEARCH_H__

#include "BinaryTree3.h"

typedef BTData BSTData;

// 이진 탐색 트리의 생성 및 초기화
void BSTMakeAndInit(BTreeNode** pRoot);

// 노드에 저장된 데이터 반환
BSTData BSTGetNodeData(BTreeNode* bst);

// 이진 탐색 트리를 대상으로 데이터 저장(노드의 생성과정 포함)
void BSTInsert(BTreeNode** pRoot, BSTData data);

// 이진 탐색 트리를 대상으로 데이터 탐색
BTreeNode* BSTSearch(BTreeNode* bst, BSTData target);

// 트리에서 노드를 제거하고 노드의 주소 값을 반환
BTreeNode* BSTRemove(BTreeNode** pRoot, BSTData target);

// 이진 탐색 트리에 저장된 모든 노드의 데이터를 출력
void BSTShowAll(BTreeNode* bst);

#endif
```

## BinarySearchTree2.c
```c
...

BTreeNode* BSTRemove(BTreeNode** pRoot, BSTData target)
{
	// 삭제 대상이 루트 노드인 경우를 별도로 고려해야 한다.
	BTreeNode* pVRoot = MakeBTreeNode();	// 가상 루트 노드
	BTreeNode* pNode = pVRoot;				// parent node
	BTreeNode* cNode = *pRoot;				// current node
	BTreeNode* dNode;

	// 루트 노드를 pVRoot가 가리키는 노드의 오른쪽 자식 노드가 되게 한다.
	ChangeRightSubTree(pVRoot, *pRoot);

	// 삭제 대상인 노드를 탐색
	while (cNode != NULL && GetData(cNode) != target)
	{
		pNode = cNode;

		if (target < GetData(cNode))
			cNode = GetLeftSubTree(cNode);
		else
			cNode = GetRightSubTree(cNode);
	}

	if (cNode == NULL)	// 삭제 대상이 존재하지 않는다면,
		return NULL;

	dNode = cNode;		// 삭제 대상을 dNode가 가리키게 한다.

	// 첫 번째 경우: 삭제 대상이 단말 노드인 경우
	if (GetLeftSubTree(dNode) == NULL && GetRightSubTree(dNode) == NULL)
	{
		if (GetLeftSubTree(pNode) == dNode)
			RemoveLeftSubTree(pNode);
		else
			RemoveRightSubTree(pNode);
	}

	// 두 번째 경우: 삭제 대상이 하나의 자식 노드를 갖는 경우
	else if (GetLeftSubTree(dNode) != NULL || GetRightSubTree(dNode) != NULL)
	{
		BTreeNode* dcNode;		// 삭제 대상의 자식 노드 가리킴

		if (GetLeftSubTree(dNode) != NULL)
			dcNode = GetLeftSubTree(dNode);
		else
			dcNode = GetRightSubTree(dNode);

		if (GetLeftSubTree(pNode) == dNode)
			ChangeLeftSubTree(pNode, dcNode);
		else
			ChangeRightSubTree(pNode, dcNode);
	}

	// 세 번째 경우: 두 개의 자식 노드를 모두 갖는 경우
	else
	{
		BTreeNode* mNode = GetRightSubTree(dNode);			// 대체 노드를 가리킴
		BTreeNode* mpNode = dNode;							// 대체 노드의 부모 노도를 가리킴
		int delData;

		// 삭제 대상의 대체 노드를 찾는다.
		while (GetLeftSubTree(mNode) != NULL)
		{
			mpNode = mNode;
			mNode = GetLeftSubTree(mNode);
		}

		// 대체 노드에 저장된 값을 삭제할 노드에 대입한다.
		delData = GetData(dNode);							// 대입 전 데이터 백업
		SetData(dNode, GetData(mNode));						// 대입

		// 대체 노드의 부모 노드와 자식 노드를 연결한다.
		if (GetLeftSubTree(mpNode) == mNode)
			ChangeLeftSubTree(mpNode, GetRightSubTree(mNode));
		else
			ChangeRightSubTree(mpNode, GetRightSubTree(mNode));

		dNode = mNode;
		SetData(dNode, delData);							// 백업 데이터 복원
	}

	// 삭제된 노드가 루트 노드인 경우에 대한 추가적인 처리
	if (GetRightSubTree(pVRoot) != *pRoot)
		*pRoot = GetRightSubTree(pVRoot);					// 루트 노드의 변경을 반영

	free(pVRoot);		// 가상 루트 노드의 소면
	return dNode;		// 삭제 대상의 변환
}

void ShowIntData(int data)
{
	printf("%d ", data);
}

void BSTShowAll(BTreeNode* bst)
{
	InorderTraverse(bst, ShowIntData);	// 중위 순회
}

```

# reference 
윤성우의 열혈 C 자료구조 - 윤성우
