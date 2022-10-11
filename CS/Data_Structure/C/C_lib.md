## 라이브러리
- C언어에서는 좀 더 효과적으로 함수를 관리할 수 있도록 라이브러리 기술을 제공한다.

- 지속적으로 업데이트가 필요한 함수들만 소스 파일에 유지하고 나머지 함수들은 라이브러리 파일에 넣어서 관리 할 수 있도록 만든 것을 말한다.
```c
// test1.c
void main()
{
    Add();
}

// test2.obj
Add 함수의 기계어
Sub 함수의 기계어

// test1.c 컴파일 
// test1.obj
main 함수의 기계어

// 링크
//test.exe
main 함수의 기계어
Add 함수의 기계어
SUb 함수의 기계어   // 사용하지 않는데 실행 파일에 포함됨

/*
오브젝트파일의 경우 모든 함수가 실행 파일에 포함
*/
```

```c
// test1.c
void main()
{
    Add();
}

// test2.lib
Add 함수의 기계어
Sub 함수의 기계어

// test1.c 컴파일 
// test1.obj
main 함수의 기계어

// 링크
//test.exe
main 함수의 기계어
Add 함수의 기계어
```

## 헤더파일
- 헤더파일은 라이브러리에 있는 함수 원형을 미리 선언해 둔 것을 말한다.
- 즉, 라이브러리의 설명서라고 생각하면 된다.
```c
// main.c 소스 파일
void main()
{
    int result1, result2, result3, result4;
    resul1 = Add(2, 3);    // 오류발생
    resul2 = Sub(2, 3);    // 오류발생
    resul3 = Mul(2, 3);    // 오류발생
    resul4 = Div(2, 3);    // 오류발생
}

// MyMath.h 헤더 파일
int Add(int value1, int value2);
int Sub(int value1, int value2);
int Mul(int value1, int value2);
int Div(int value1, int value2);

// MyMath.lib 라이브러리 파일
Add, Sub, Mul, Div 함수는 존재하지만, 기계어로 되어있어서 내용을 확인할 수 없다.

/*
함수 원형이 헤더 파일에 선언되었지만, main.c소스파일에는 사용할 함수 원형이 선언되지 않아서 오류가 발생
main.c소스파일에서 각 함수를 사용하기 전에 컴파일러에 MyMath.h 헤더 파일을 먼저 읽도록 지시해야 한다.
*/
```

## 전처리기
- 원하는 사항을 컴파일러에 직접 지시하는 문법을 전처리기라 한다.
- `#` 기호로 시작하고, `;`을 사용하지 않는다.

### #include 전처리기
- 컴파일러에 자신이 명시한 파일을 읽도록 지시
- #include "읽을 파일 이름"

#include <헤더 파일 이름>|비주얼 스튜디오에서 제공하는 헤더 파일을 포함
--|--
#include "헤더 파일 이름"|프로그래머가 정의해 사용하는 헤더 파일을 포함

### #define 전처리기
- 상수나 명령문을 치환하는 문법
```c
// #define 문법으로 상수 치환
#define Max_COUNT 3 
/*
Max_count - 치환할 이름
3 - 치환될 내용
*/
```
```c
// #define 문법으로 명령 치환
#define POW_VALUE(a) (a * a)
int data = POW_VALUE(3);    // int data = (3 * 3)으로 번역

// (a * a) 명령을 의미
```

## 표준라이브러리
### putchar
- 단일 문자 출력
```c
#include <stdio.h>

void main()
{
    putchar('H');
    putchar('e');
    putchar('l');
    putchar('l');
    putchar('o');
    putchar('!');
}
```
### puts
```c
#include <stdio.h>

void main()
{
    puts("Hi!");    //  출력 후 줄바꿈도 동시에 이루어짐
}
```
- 문자열 출력 함수
### printf



# reference
DO it! C언어 입문 - 김성엽  
동영상 강좌 - 'Do it! C언어 입문' - 6장   
https://www.youtube.com/watch?v=9P-E2vwJW4M&list=PLiZvlxkcLhakQwbPjkyfuHFy1IVG-VXrP&index=6
