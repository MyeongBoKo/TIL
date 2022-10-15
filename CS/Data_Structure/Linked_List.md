## 정적인 배열
```c
#include <stdio.h> 

int main(void)
{
	int arr[10];
	int readCount = 0;
	int readData;
	int i;

	while (1) {
		printf("자연수 입력: ");
		scanf_s("%d", &readData);
		if (readData < 1)
			break;

		arr[readCount++] = readData;
	}

	for (i = 0; i < readCount; i++)
		printf("%d ", arr[i]);
}
```

## 동적인 메모리 구성
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct __node
{
	int data;
	struct __node* next;
} Node;

int main(void)
{
	Node* head = NULL;
	Node* tail = NULL;
	Node* cur = NULL;

	Node* newNode = NULL;
	int readData;

	while (1) {
		printf("자연수 입력: ");
		scanf_s("%d", &readData);
		if (readData < 1)
			break;

		newNode = (Node*)malloc(sizeof(Node));
		newNode->data = readData;
		newNode->next = NULL;

		if (head == NULL)
			head = newNode;
		else
			tail->next = newNode;

		tail = newNode;
	}
	printf("\n");

	printf("입력 받은 데이터의 전체출력! \n");
	if (head == NULL)
		printf("저장된 자연수가 존재하지 않습니다. \n");
	else {
		cur = head;
		printf("%d ", cur->data);

		while (cur->next != NULL) {
			cur = cur->next;
			printf("%d ", cur->data);
		}
	}
	printf("\n\n");

	if (head == NULL)
		return 0;
	else {
		Node* delNode = head;
		Node* delNextNode = head->next;

		printf("%d을(를) 삭제합니다. \n", head->data);
		free(delNode);

		while (delNextNode != NULL) {
			delNode = delNextNode;
			delNextNode = delNextNode->next;

			printf("%d을(를) 삭제합니다. \n", delNode->data);
			free(delNode);
		}
	}
	return 0;
}

```

# reference 
윤성우의 열혈 자료구조 - 윤성우
