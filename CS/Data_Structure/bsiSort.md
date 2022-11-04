# 정렬
### 정렬
- 정렬시켜야 할 대상은 레코드라고 불린다.

- 레코드는 다시 필드라는 단위로 나뉜다.
- 정렬은 레코드들을 키값의 순서로 재배열하는 것을 말한다.
- 정렬 알고리즘은 많이 개발되었지만, 최상의 성능을 보여주는 최적의 알고리즘은 존재하지 않는다.
- 현재 프로그램 수행환경에서 가장 효율적인 정렬 알고리즘을 프로그래머가 선택해서 사용해야 한다.
- 효율성의 기준은 비교 연산 횟수, 이동 연산의 회수를 빅오 표기법으로 근사적으로 표현한다.

### 정렬 알고리즘
- 단순하지만 비효율적인 알고리즘
  - 삽입 정렬, 선택 정렬, 버블 정렬

- 복잡하지만 효율적인 알고리즘
  - 퀵 정렬, 히프 정렬, 합병 정렬, 기수 정렬 등 
- 내부정렬  
  - 정렬하기 전 모든 데이터가 메인 메모리에 올라와 있는 정렬
- 외부정렬
  - 외부 기억 장치에 대부분의 데이터가 있고, 일부만 메모리에 올려놓은 상태에서 정렬

### 정렬 알고리즘에서 안정성
- 안정성이란 입력 데이터에 동일한 키값을 값는 레코드가 여러 개 존재하는 경우 레코드들의 상대적인 위치가 정렬 후에도 바뀌지 않는 것을 의미
- 레코드들의 상대적인 위치가 바뀌게 되면 안정하지 않음을 의미

## 버블 정렬

### 버블 정렬 성능 평가
- 데이터간의 비교연산의 경우 
  - 최악의 경우 O(n^2)
  - 최선의 경우 O(n^2)

- 데이터간의 이동횟수의 경우
  - 최악의 경우 O(n^2), 이때 데이터 이동횟수는 비교횟수보다 3배 더 많다.
  - 최선의 경우 x
### 버블 정렬 구현
```c
#include <stdio.h>

void BubbleSort(int arr[], int n)
{
	int i, j;
	int temp;

	for (i = 0; i < n - 1; i++)
	{
		for (j = 0; j < (n - i) - 1; j++)
		{
			if (arr[j] > arr[j + 1])
			{
				temp = arr[j];
				arr[j] = arr[j + 1];
				arr[j + 1] = temp;
			}
		}
	}
}

int main(void)
{
	int arr[4] = { 3, 2, 4, 1 };
	int i;

	BubbleSort(arr, sizeof(arr) / sizeof(int));

	for (i = 0; i < 4; i++)
		printf("%d ", arr[i]);

	printf("\n");
	return 0;
}
```

## 선택 정렬
### 선택 정렬 원리
- 정렬이 완료된 숫자들의 리스트, 정렬이 되지 않은 숫자들이 있는 리스트 2개가 있다고 가정한다.
- 정렬이 되지 않은 숫자들의 리스트에서 가장 작은 숫자를 선택해서 정렬이 완료된 숫자들의 리스트로 옮긴다
- 이 작업을 반복해서 결과를 도출하는 정렬이다.

### 선택 정렬 분석
- 바깥 for은 n-1번 실행, 안쪽 for은 0에서 n-2번까지 반복 즉, (n-1)-i번 반복
- 전체 비교 횟수는 안쪽 for로 결정되므로 O(n^2)
  - 최악의 경우 O(n^2)
  - 최선의 경우 O(n^2)
- 전체 이동 횟수는 3(n-1), O(n) 
  - 최악의 경우 O(n)
  - 최선의 경우 O(n)

### 선택 정렬 구현
```c
#include <stdio.h>

void SelSort(int arr[], int n)
{
	int i, j;
	int maxIdx;
	int temp;

	for (i = 0; i < n - 1; i++)
	{
		maxIdx = i;

		for (j = i + 1; j < n; j++)
		{
			if (arr[j] < arr[maxIdx])
				maxIdx = j;
		}

		temp = arr[i];
		arr[i] = arr[maxIdx];
		arr[maxIdx] = temp;
	}
}

int main(void)
{
	int arr[4] = { 3, 4, 2, 1 };
	int i;

	SelSort(arr, sizeof(arr) / sizeof(int));

	for (i = 0; i < 4; i++)
		printf("%d ", arr[i]);

	printf("\n");
	return 0;
}

```

## 삽입 정렬 

### 삽입 정렬 순서
1. 인덱스 1부터 시작한다. 이때 인덱스 0은 이미 정렬된 것으로 본다.
2. 현재 삽입될 숫자인 i번째 정수를 key변수로 복사한다.
3. 현재 정렬된 배열은 i-1까지 이므로 i-1번째부터 역순으로 조사한다.
4. j값이 음수가 아니어야 되고 key값보다 정렬된 배열에 있는 값이 크면
5. j번째를 j+1번째로 이동한다.
6. j를 하나 감소한다.
7. j번째 정수가 key보다 작으므로 j+1번째가 key값이 들어갈 위치이다.

### 삽입 정렬 성능
- 데이터의 이동횟수
  - 최선의 경우 x
  - 최악의 경우 O(n^2)

- 데이터의 비교횟수
  - 최선의 경우 x
  - 최악의 경우 O(n^2)
   
### 삽입 정렬 구현
```c
#include <stdio.h>

void InsertSort(int arr[], int n)
{
	int i, j;
	int insData;

	for (i = 1; i < n; i++)
	{
		insData = arr[i];

		for (j = i - 1; j >= 0; j--)
		{
			if (arr[j] > insData)
				arr[j + 1] = arr[j];
			else
				break;
		}

		arr[j + 1] = insData;
	}
}

int main(void)
{
	int arr[5] = { 5,3,2,4,1 };
	int i;

	InsertSort(arr, sizeof(arr) / sizeof(int));

	for (i = 0; i < 5; i++)
		printf("%d ", arr[i]);

	printf("\n");
	return 0;
}
```

# reference
윤성우의 열혈 자료구조 - 윤성우   
C언어로 쉽게 풀어쓴 자료구조 - 천인국
