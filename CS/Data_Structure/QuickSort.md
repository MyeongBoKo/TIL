# 퀵 정렬
- 분할 정복에 근거하여 만들어진 정렬 방법
- 평균적으로 매우 빠른 정렬의 속도를 보이는 알고리즘

## 이해 및 구현
- 오른차순 정렬을 기준으로 구현
  
- `left`: 정렬대상의 가장 왼쪽 지점을 의미
- `right`: 정렬대상의 가장 오른쪽 지점을 의미
- `pivot`: 피벗이라 불림, 중심점 즉 중심축의 의미를 갖음, 정렬하는데 필요한 기준
- `low`: 피벗을 제외한 가장 왼쪽에 위치한 지점을 의미
  - `low`의 오른쪽 방향 이동 - 피벗보다 큰 값을 만날 때까지(피벗보다 정렬의 우선순위가 낮은 데이터를 만날 때까지)
- `high`: 피벗을 제외한 가장 오른쪽에 위치한 지점을 의미
  - `high`의 왼쪽 방향 이동 - 피벗보다 작은 값을 만날 때까지(피벗보다 정렬의 우선순위가 높은 데이터를 만날 때까지)

- low와 high가 가리키는 위치가 교차되는 상황일 때, `Swap(arr, low, high);`을 통해서 low와 high의 위치를 바꾼다. 이때 인덱스 값은 바뀌지 않고 low와 high의 위치만 바뀜

- `Swap(arr, left, high);` 피벗과 high가 가리키는 대상이 교환된다. 이 코드를 통해서 피벗이었던 값이 정렬된다.

```c
	while (low <= high)     // 항상 '참'일 수밖에 없는 상황
	{
		while (pivot > arr[low])    // 문제가 되는 지점
			low++;

		while (pivot < arr[high])   // 문제가 되는 지점
			high--;

		if (low <= high)
			Swap(arr, low, high);
	}
```
- `pivot == arr[low] = arr[high]`의 경우 바깥쪽 while문을 탈출하지 못해서 오류가 발생한다.
```c
	while (low <= high)
	{
		while (pivot > arr[low] && low <= right)
			low++;

		while (pivot < arr[high] && high >= (left + 1))
			high--;

		if (low <= high)
			Swap(arr, low, high);
	}
```

## 메인
```c
#include  <stdio.h>

void Swap(int arr[], int idx1, int idx2)
{
	int temp = arr[idx1];
	arr[idx1] = arr[idx2];
	arr[idx2] = temp;
}

int Partition(int arr[], int left, int right)
{
	int pivot = arr[left];
	int low = left + 1;
	int high = right;

	while (low <= high)
	{
		while (pivot > arr[low])
			low++;

		while (pivot < arr[high])
			high--;

		if (low <= high)
			Swap(arr, low, high);
	}

	Swap(arr, left, high);
	return high;
}

void QuickSort(int arr[], int left, int right)
{
	if (left <= right)
	{
		int pivot = Partition(arr, left, right);
		QuickSort(arr, left, pivot - 1);
		QuickSort(arr, pivot + 1, right);
	}
	
}

int main(void)
{
	int arr[7] = { 3,2,4,1,7,6,5 };

	int len = sizeof(arr) / sizeof(int);
	int i;

	QuickSort(arr, 0, sizeof(arr)/sizeof(int) - 1);

	for (i = 0; i < len; i++)
		printf("%d ", arr[i]);

	printf("\n");
	return 0;
}
```

# reference
윤성우의 열혈 C 자료구조 - 윤성우
