# ▣ 배열
## 1. 배열이란
- 데이터를 그룹을 묶어서 표현하는 것을 말함.

## 2. 배열 선언 및 사용
### ■ 배열 선언 
`short grade[n];`   

- 2바이트 정수형 데이터 n개를 저장할 수 있는 배열을 grade라는 이름으로 선언

short|grade|[n]|
--|--|--
자료형|변수 이름| 요소 개수
- `[](대괄호)`를 통해서 저장 공간을 몇 개 만들지 명시함. 이때 개수는 상수로 나타내야 함.
- 상수로 나타내지 않고 변수로 나타낸다면 컴파일러가 변수의 크기를 결정할 수 없기 때문에 오류를 발생시킴.


grade[0]|grade[1]|grade[2]|grade[3]|...|grade[n-1]
--|--|--|--|--|--
short형|short형|short형|short형|short형|short형

- 배열의 시작은 0부터 시작함.
- grade의 배열의 크기는 2바이트 * n개. 즉 2n을 의미함. 

### ■ 배열의 특정 요소에 값 대입 
`grade[1] = 80;`

grade|[1]| = 80
--|--|--
배열 이름|인덱스(값을 대입할 위치)|대입할 값

grade[0]|grade[1]|grade[2]|grade[3]|...|grade[n-1]
--|--|--|--|--|--
| |80|
short형|short형|short형|short형|short형|short형

### ■ 배열의 초기화
- 배열을 전역 변수로 선언하면 자동으로 0으로 초기화 되지만, 배열 문법은 지역 변수를 그룹으로 묶은 것이기 때문에 지역 변수와 같이 자동으로 초기화되지 않는다.
  
- 배열의 요소에 값을 대입할 때 직접 대입할 수 있지만, 무수히 많은 배열의 경우 직접 대입하기가 어려운 경우 반복문을 이용해서 나타낼 수 있음.
```c
// 반복문을 이용해서 grade의 배열의 모든 요소를 0으로 초기화.
// 이때 grade의 배열의 크기는 10함. 
#include <stdio.h>

void main()
{
    short grade[10], i;
    for (i = 0; i < 10; i++) grade[i] = 0;

    grade[1] = 80;
    printf("%d %d\n", grade[1], grade[9]);
}

/*
80 0
*/
```

- 배열을 반복문을 통해 초기화를 매번하는 것은 쉬운 일이 아니다. 그래서 쉼표를 사용해서 배열을 초기화하는 방법이 존재한다.<br>
```c
short grade[10] = {0, 0, 0, 0, 0, 0, 0, 0, 0, 0};
short grade[10] = {0,};     // 위의 코드와 결과값은 같다.

short grade[5] = {90,};     // short grade[5] = {90, 0, 0, 0, 0};
```
- 배열의 크기는 생략가능하다.
- 컴파일러가 자동적으로 배열의 크기를 인식해서 처리한다.
```c
short grade[] = {90, 80, 85, 60, 100};  

// 위의 코드와 같다.
short grade[5] = {90, 80, 85, 60, 100};  
```
### ■ 배열의 요소 값 사용
```c
short data[3];
data[0] = 2;                    // 배열의 0번째 요소에 2를 대입
data[1] = data[0] + 5;          // 배열의 1번째 요소에 7가 저장
data[2] = data[0] + data[1];    // 베열의 2번째 요소에 9가 저장
```
# ▣ 문자열
### ■ 문자열을 표현할 때 char을 사용하는 이유
- 문자열을 저장하려면 char을 사용하는 것이 적합하다.

- char가 실제로 저장할 수 있는 크기가 sign의 경우 -128 ~ 127, unsign의 경우 0 ~ 255이다.
- 아스키코드의 경우 0에서 255번 사이에만 존재한다. 이때 아스키코드는 문자열을 표현하는 코드이다
- 문자열을 저장하기 위해 적합한 크기는 1byte이고, 1byte를 대변하는 것은 char이기 때문이다. 그래서 c언어에서 문자는 char로 사용하는 것이 적합하다.

### ■ 문자열을 배열로 표현하는 이유
- 문자열을 배열로 표현하지 않는 경우 일일이 1바이트 char형 변수를 각각 선언 후 그 변수에 문자를 저장해야 한다. 하지만 무수히 많은 문자열을 표현해야 하는 경우에는 이렇게 사용하는 것은 불가능하다.

- 문자열을 배열로 표현해서 불편을 덜 수 있다.

### ■ 배열을 통해 문자열을 표현하는 방법
```c
char data[6] = { 'h', 'a', 'p', 'p', 'y', 0 };
// 문자의 개수는 5이고 마지막에 0을 추가해서 배열의 크기는 6

char data[6] = "happy";
// 문자열의 마지막에 NULL(0)이 컴파일러에 의해 자동으로 추가
```
- 문자의 끝에 NULL(널) 문자 0 을 추가 입력해서 ' 이 배열에 저장된 정보는 문자열이다.' 라고 컴파일러에게 알림

### ■ 저장된 문자열의 길이 구하는 방법
- 문자열의 마지막은 0이기 때문에 0이 나올때까지 반복해서 구하면 길이를 구할 수 있다.
```c
char data[6] = "happy";
int count = 0;
while (data[count] != 0) {  
    count++;    
}
// 문자열이 0이 나올때까지 증가시켜서 반복시킴
```

### ■ 내장함수
- str로 시작하는 문자열 표준 함수들은 `#include` 전처리기로 string.h 파일을 소스 파일안에 포함시켜 사용
- `strlen(문자열이 저장된 변수 이름)`<br>
  :문자열의 길이를 구하는 내장함수
- `strcpy(복사해서 저장할 변수 이름, 복사할 기존 변수 이름)` <br> 
  :문자열을 복사하는 내장함수
- `strcat(기존 문자열이 저장된 변수 이름, 새로 덧붙일 문자열)` <br> 
  :문자열을 추가하는 내장함수

# ▣ 2차원 배열
### ■ 2차원 배열 선언
  `char data[5][4]`
- char은 자료형
- data는 변수 이름
- [5] 행 개수(그룹 개수)
- [4] 열 개수(그룹당 세부 요소 개수)

  

data[0][0]| data[0][1] | data[0][2] |data[0][3]
--|--|--|--

data[1][0]| data[1][1]| data[1][2]|data[1][3]
--|--|--|--

data[2][0]| data[2][1]| data[2][2]|data[2][3]
--|--|--|--

data[3][0]| data[3][1]| data[3][2]|data[3][3]
--|--|--|--
 
data[4][0]| data[4][1]| data[4][2]|data[4][3]
--|--|--|--

```c
char data1, data2, data3, data4;                // 4개의 변수를 개별적으로 선언

char data[4];             // 4개의 변수를 그룹으로 묶어서 1차원 배열 형태로 선언

char data1[4], data2[4], data3[4], data4[4], data5[4]; // char[4] 형식의 1차원 배열 5개를 선언

char data[5][4];       // char[4] 형식의 1차원 배열 5개를 묶어 2차원 배열로 선언                       
```

### ■ 2차원 배열을 컴파일러가 해석하는 순서
1. char (data[5])[4];<br>
: 연산자 우선순위에 의해 먼저 data[5]가 먼저 수행, 5개의 요소를 가지는 배열을 만듬

2. char (data[5])[4];<br>
: char [4]가 수행, 즉 배열의 각 요소가 char[4] 크기를 갖는다.

- 컴파일러는 2차원 배열을 1차원 배열로 변환해서 해석한다.
  
data[0][0]|ㅇ|ㅇ|ㅇ|data[1][0]|ㅇ|ㅇ|ㅇ|data[2][0]|ㅇ|ㅇ|ㅇ|data[3][0]|ㅇ|ㅇ|ㅇ|data[4][0]|ㅇ|ㅇ|ㅇ
--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--

### ■ 2차원 배열 초기화
```c
char temp[2][3] = {{1, 2, 3}, {4, 5, 6}};
```

temp[0][0]<br> 1 |temp[0][1]<br> 2 |temp[0][2]<br> 3
:--:|:--:|:--:
temp[1][0]<br> 4 |temp[1][1]<br> 5 |temp[1][2]<br> 6


# reference
Do it! C언어 입문 - 김성엽<br>
'Do it! C언어 입문' 12장 배열과 문자열 (1/2)   
https://www.youtube.com/watch?v=nQ73Yu9hfjQ&list=PLiZvlxkcLhakQwbPjkyfuHFy1IVG-VXrP&index=15   
'Do it! C언어 입문' - 12장 배열과 문자열 (2/2)   
https://www.youtube.com/watch?v=wAITao6TnNs&list=PLiZvlxkcLhakQwbPjkyfuHFy1IVG-VXrP&index=15