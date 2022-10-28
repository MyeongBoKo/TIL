## 이진트리
- 이진 트리 조건
  - 루트 노드를 중심으로 두 개의 서브 트리로 나뉜다
  
  - 나뉘어진 두 서브 트리도 모두 이진 트리다
- 이진 트리란 루트 노드를 중심으로 둘로 나뉘는 두 개의 서브 트리도 이진 트리어야 하고, 그 서브 트리의 모든 서브 트리도 이진 트리여야 한다.

- 노드가 위치할 수 있는 공간에 노드가 존재하지 않으면, 공집합 노드가 있다고 간주하기 때문에 공집합 노드도 이진 트리의 판단에 있어서 노드로 인정한다.

## 포화 이진 트리 & 완전 이진 트리
- 레벨 - 각 층별로 숫자를 매기는데 이때 트리의 레벨이라 한다.
- 높이 - 트리의 최고 레벨을 높이라 한다.

### 포화 이진 트리
- 포화 이진 트리란 모든 레벨이 꽉 차 있다.
- 노드를 더 추가하려면 레벨을 늘려야 한다.
- 모든 레벨이 꽉 찬 이진 트리를 포화 이진 트리라 한다.

### 완전 이진 트리
- 포화 이진 트리처럼 모든 레벨이 꽉 찬 상태는 아니지만, 빈 틈 없이 노드가 꽉찬 트리를 말한다.

## 이진 트리 자료구조의 ADT
```c
BTreeNode* MakeBTreeNode(void);
- 이진 트리 노드를 생성하여 그 주소 값을 반환 

BTData GetData(BTreeNode* bt);
- 노드에 저장된 데이터를 반환

void SetData(BTreeNode* bt, BTData data);
- 노드에 데이터를 저장한다. data로 전달된 값을 저장한다.

BTreeNode* GetLeftSubTree(BTreeNode* bt);
- 왼쪽 서브 트리의 주소 값을 반환한다.

BTreeNode* GetRightSubTree(BTreeNode* bt);
- 오른쪽 서브 트리의 주소 값을 반환한다.

void MakeLeftSubTree(BTreeNode* main, BTreeNode* sub);
- 왼쪽 서브 트리를 연결한다.

void MakeRigthSbTree(BTreeNode* main, BTreeNode* sub);
- 오른쪽 서브 트리를 연결한다.
```

## 헤더파일
```c
#ifndef __BINARY_TREE_H__
#define __BINARY_TREE_H__

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
void MakeRigthSbTree(BTreeNode* main, BTreeNode* sub);

#endif
```

## 소스파일
```c
#include <stdio.h>
#include <stdlib.h>
#include "BinaryTree.h"

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
```

## 메인
```c
#include <stdio.h>
#include "BinaryTree.h"

int main(void)
{
	BTreeNode* bt1 = MakeBTreeNode();
	BTreeNode* bt2 = MakeBTreeNode();
	BTreeNode* bt3 = MakeBTreeNode();
	BTreeNode* bt4 = MakeBTreeNode();

	SetData(bt1, 1);
	SetData(bt2, 2);
	SetData(bt3, 3);
	SetData(bt4, 4);

	MakeLeftSubTree(bt1, bt2);
	MakeRigthSbTree(bt1, bt3);
	MakeLeftSubTree(bt2, bt4);

	printf("%d \n", GetData(GetLeftSubTree(bt1)));

	printf("%d \n", GetData(GetLeftSubTree(GetLeftSubTree(bt1))));

	return 0;
}
```

# reference
윤성우의 열혈 자료구조 - 윤성우
