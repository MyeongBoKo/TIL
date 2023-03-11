# 순차탐색
- 정렬의 여부에 상관없이 사용할 수 있는 탐색 알고리즘
- 데이터가 N개일 때, 시간복잡도가 최악의 경우 O(N)

## 구현
### 1. C언어로 구현
```c
#include <stdio.h>

int LSearch(int ar[], int len, int target)
{
	int i;
	for (i = 0; i < len; i++)
	{
		if (ar[i] == target)
			return i;
	}
	return -1;
}

int main(void)
{
	int arr[] = { 3, 5, 2, 4, 9 };
	int idx;

	idx = LSearch(arr, sizeof(arr) / sizeof(int), 4);
	if (idx == -1)
		printf("탐색 실패\n");
	else
		printf("타겟 저장 인덱스:%d\n", idx);

	idx = LSearch(arr, sizeof(arr) / sizeof(int), 7);
	if (idx == -1)
		printf("탐색 실패\n");
	else
		printf("타겟 저장 인덱스:%d\n", idx);

	return 0;
}
```

### 2. python으로 구현
```python
def LSearch(ar, target):
    arLen = len(ar)

    for i in range(arLen):
        if ar[i] == target:
            return i
    return -1

arr = [3, 5, 2, 4, 9]
idx = LSearch(arr, 4)

if idx == -1:
    print("Fail")
else:
    print("Index number is %d" %idx)
```

# 이진탐색
- 데이터가 정렬되어야 사용할 수 있는 탐색 알고리즘
- 배열의 시작점, 끝점, 중간점을 반복적으로 사용해서 구하는 알고리즘
- 시작점 > 끝점일 때 탐색을 종료
- 시간복잡도 O(logN)

## 구현
### 1. C로 구현
```c
#include <stdio.h>

int BSearch(int ar[], int len , int target)	// 배열, 찾는 값
{
	int first = 0;
	int last = len - 1;
	int mid;

	while (first <= last)
	{
		mid = (first + last) / 2;

		if (target == ar[mid])
		{
			return mid;
		}

		else
		{
			if (target < ar[mid])
				last = mid - 1;
			else
				first = mid + 1;
		}
	}

	return -1;
}

int main(void)
{
	int arr[] = { 1, 3, 5, 7, 9 };
	int idx;

	idx = BSearch(arr, sizeof(arr) / sizeof(int), 7);
	if (idx == -1)
		printf("탐색을 실패하였습니다.\n");
	else
		printf("idx[%d] = %d\n", idx, arr[idx]);

	idx = BSearch(arr, sizeof(arr) / sizeof(int), 4);
	if (idx == -1)
		printf("탐색을 실패하였습니다.\n");
	else
		printf("idx[%d] = %d\n", idx, arr[idx]);

}
```

### 2. python으로 구현
```python
# 반복문 사용
def BSearch(ar, target):
    arLen = len(ar)

    first = 0
    last = arLen - 1

    while (first <= last):
        mid = (first + last) // 2

        if ar[mid] == target:
            return mid
        else:
            if target < ar[mid]:
                last = mid - 1
            else:
                first = mid + 1

    return - 1


arr = [1, 3, 5, 7, 9]
idx = BSearch(arr, 7)

if idx == -1:
    print("Fail")
else:
    print("Index number is %d" %idx)

```

```python
# 재귀 사용
def BSearch(arr, target, start, end):
    if start > end:
        return -1

    middle = (start + end) // 2
    if arr[middle] == target:
        return middle
    elif arr[middle] > target:
        return BSearch(arr, target, start, middle - 1)
    else:
        return BSearch(arr, target, middle + 1, end)


arr = [1, 3, 5, 7, 9]
idx = BSearch(arr, 7, 0, len(arr)-1)

if idx == -1:
    print("Fail")
else:
    print("Index number is %d" %idx)
```

# reference
윤성우의 열혈 자료구조 - 윤성우<br>
https://techblog-history-younghunjo1.tistory.com/181
