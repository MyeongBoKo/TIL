## 보간 탐색
- 이진탐색의 경우 찾는 대상이 중앙에 위치하건 그에 상관없이 일관되게 반씩 줄여나가는 탐색
- 이때 찾는 위치에 따라 효율이 달라짐
- 비효율성을 개선한 것이 보간 탐색
- 보간 탐색은 데이터의 값과 그 데이터가 저장된 위치의 인덱스 값이 비례한다고 가정
- 
## 메인
```c
#include <stdio.h>

int ISearch(int arr[], int first, int last, int target)
{
	int mid;

	if (arr[first]>target||arr[last]<target)
		return -1;		// -1의 반환은 탐색의 실패를 의미

	// 이진 탐색과의 차이점을 반영한 문장
	mid = ((double)(target - arr[first]) / (arr[last] - arr[first]) * (last - first)) + first;

	if (arr[mid] == target)
		return mid;
	else if (target < arr[mid])
		return ISearch(arr, first, mid - 1, target);
	else
		return ISearch(arr, mid + 1, last, target);
}

int main(void)
{
	int arr[] = { 1,3,5,7,9 };
	int idx;

	idx = ISearch(arr, 0, sizeof(arr) / sizeof(int) - 1, 7);
	if (idx == -1)
		printf("탐색 실패 \n");
	else
		printf("탐색 저장 인텍스: %d \n", idx);

	idx = ISearch(arr, 0, sizeof(arr) / sizeof(int) - 1, 10);
	if(idx == -1)
		printf("탐색 실패 \n");
	else
		printf("탐색 저장 인텍스: %d \n", idx);
}
```

# reference
윤성우의 열혈 C자료구조 - 윤성우
