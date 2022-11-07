# 병합 정렬
- 분할 정복이라는 알고리즘 디자인 기법에 근거하여 만들어진 정렬 방법
- 1단계 분할, 2단계 정복, 3단계 결합

## MergeSort
```
void MergeSort(int arr[], int left, int right)
    if (left가 right보다 작은 경우)
        mid = (left+right)/2

        MergeSort(arr, left, mid)       - 재귀
        Mergesort(arr, mid+1, right)    - 재귀

        MergeTwoArea(arr, left, mid, rigt)
```

## MergeTwoArea
```
void MergeTwoArea(arr[], int left, int mid, int right)
    int fIdx = left
    int rIdx = mid+1
    int i
    병합 한 결과를 담을 배열 sortArr의 동적 할당
    int sidx = left

    while (fIdx<=mid && rIdx<=right의 경우)
        if (arr[fidx]의 값이 arr[rIdx] 값보다 작거나 같은 경우)
            SortArr[sIdx]에 arr[fIdx] 값을 옮김, fIdx 값 증가(fIdx++)
        else
            SortArr[sIdx]에 arr[rIdx] 값을 옮김, rIdx 값 증가(rIdx++)
        
        sIdx++

    if (fIdx>mid) // 배열의 앞부분이 모두 sortArr에 옮겨졌다면
        for i가 rIdx에서 right값 까지, i++, sIdx++
            sortArr[sIdx]에 arr[i]값을 옮김
    else
        for i가 fIdx에서 mid값 까지, i++, sIdx++
            sortArr[sIdx]에 arr[i]값을 옮김

    for i가 left에서 right값 까지 반복해서 - 임시 배열에 저장된 데이터 이동
        arr[i]에 sortArr[i] 값을 옮김

    free(sortArr)
```
## 메인
```c
#include <stdio.h>
#include <stdlib.h>

void MergeTwoArea(int arr[], int left, int mid, int right)
{
	int fIdx = left;
	int rIdx = mid + 1;
	int i;

	int* sortArr = (int*)malloc(sizeof(int) * (right + 1));
	int sIdx = left;

	while (fIdx <= mid && rIdx <= right)
	{
		if (arr[fIdx] <= arr[rIdx])
			sortArr[sIdx] = arr[fIdx++];
		else
			sortArr[sIdx] = arr[rIdx++];

		sIdx++;
	}

	if (fIdx > mid)		// 배열의 앞부분이 모두 sortArr에 옮겨짐
	{
		for (i = rIdx; i <= right; i++, sIdx++)
			sortArr[sIdx] = arr[i];
	}
	else
	{
		for (i = fIdx; i <= mid; i++, sIdx++)
			sortArr[sIdx] = arr[i];
	}

	for (i = left; i <= right; i++)
		arr[i] = sortArr[i];

	free(sortArr);
}


void MergeSort(int arr[], int left, int right)
{
	int mid;

	if (left < right)
	{
		mid = (left + right) / 2;

		MergeSort(arr, left, mid);
		MergeSort(arr, mid + 1, right);

		MergeTwoArea(arr, left, mid, right);
	}
}

int main(void)
{
	int arr[7] = { 3,2,4,1,7,6,5 };
	int i;

	MergeSort(arr, 0, sizeof(arr) / sizeof(int) - 1);

	for (i = 0; i < 7; i++)
		printf("%d ", arr[i]);

	printf("\n");
	return 0;
}
```

# reference 
윤성우의 열혈 c 자료구조 - 윤성우
