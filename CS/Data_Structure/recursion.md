# 정수 팩토리얼
```c
int factorial(int n)
{
    if (n <= 1) return(1);
    else return (n * factorial(n-1));   // n은 해결된 부분, factorial(n-1) 남아있는 부분
}
```
### factorial(3) 호출
```c
int factorial(3)
{
    if (3 <= 1) return 1;
    else return (3 * factorial(2));
}
```
```c
int factorial(2)
{
    if (2 <= 1) return(1);
    else return (2 * factorial(1));
}
```
```c
int factorial(1)
{
    if (1 <= 1) return(1);
    ...
}
```
```c
factorial(3) = 3 * factorial(2)
             = 3 * 2 * factorial(1)
             = 3 * 2 * 1
             = 3 * 2
             = 6 
```
- 순환 알고리즘 구조의 경우 1) 순환 호출하는 부분 2) 순환을 멈추는 부분이 존재하는데 이때 2) 없으면 프로그램이 시스템의 오류가 발생할 때까지 무한정 호출하게 된다.

# 거듭제곱값 계산
```
power(x, n):
    if n == 0
        then return 1;
    else if n이 짝수
        then return power(x*x, n/2);
    else if ndl 홀수
        then return x * power(x*x, (n-1)/2);
```
## 순환문
```c
power(x, n)
{
    if (n == 0) return 1;
    else if ((n % 2) == 0)
        return power(x*x, n/2)
    else rturn x * power(x*x, (n-1)/2)
}
```

## 반복문
```c
double slow_power(double x, int n)
{
    int i;
    double result = 1.0;

    for (i = 0; i <n, i++)
        result = result * x;
    return(result);
}
```
# 피보나치 수열
```c
int fibo(int n)
{
    if (n == 0) {
        return 0;
    }
    else if (n == 1) {
        return 1;
    }
    else {
        return fibo(n-2) + fibo(n-1);
    } 
}
```

# 이진탐색 재귀이용
```c
#include <stdio.h>

int BS_Recursive(int ar[], int first, int last, int target)
{
	int mid;
	if (first > last)
		return -1;

	mid = (first + last) / 2;

	if (ar[mid] == target)
		return mid;
	else if (ar[mid] > target)
		BS_Recursive(ar, first, mid - 1, target);
	else
		BS_Recursive(ar, mid + 1, last, target);
}

int main()
{
	int arr[] = { 1, 3, 5, 7, 9 };
	int idx;
	int len = sizeof(arr) / sizeof(int) - 1;
	
	idx = BS_Recursive(arr, 0, len, 7);

	if (idx == -1)
		printf("탐색을 실패하였습니다.\n");
	else
		printf("탐색 저장 인덱스: %d\n", idx);

	idx = BS_Recursive(arr, 0, len, 4);

	if (idx == -1)
		printf("탐색을 실패하였습니다.\n");
	else
		printf("탐색 저장 인덱스: %d\n", idx);

	return 0;
}


```

# 하노이탑
```
// 막대 from에 쌓여있는 n개의 원판을 막대 tmp를 사용하여 막대 to로 옮긴다.
void hanoi_tower(int n, char from, char tmp, char to)
{
    if (n == 1){
        from에 있는 한 개의 원판을 to로 옮김
    }
    else{
        1) from에 맨 밑의 원판을 제외한 나머지를 tmp로 옮김
        2) from에 있는 한 개의 원판을 to로 옮김
        3) tmp의 원판들을 to로 옮김
    }
}
```
```c
#include <stdio.h>

void hanoi_tower(int n, char from, char tmp, char to)
{
	if (n == 1) {
		printf("원판 1을 %c 에서 %c으로 옮긴다.\n", from, to);
	}
	else {
		hanoi_tower(n - 1, from, to, tmp);
		printf("원판 %d을 %c에서 %c으로 옮긴다.\n", n, from, to);
		hanoi_tower(n - 1, from, to, tmp);
	}
}

int main(void)
{
	hanoi_tower(4, 'a', 'b', 'c');
	return 0;
}
```

# reference
C언어로 쉽게 풀어쓴 자료구조 - 천인국   
윤성우의 열혈 자료구조 - 윤성우
