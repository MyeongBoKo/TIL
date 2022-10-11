# 자료형
- c언어에서는 메모리를 사용할 때 몇 바이트의 메모리를 사용할 것인지 명시해야 한다.
- 이때 이것을 데이터 타입 또는 자료형이라 한다.
- 정수형 & 실수형

## 정수형
정수 형식의 자료형|부호의 유무| 저장할 수 있는 범위
:--:|:--:|:--:
char|signed char|-128 ~ 127
 ''|unsigned char|0~255

 정수 형식의 자료형|저장 공간의 크기|부호의 유무| 저장할 수 있는 범위
:--:|:--:|:--:|:--:
int|short int|signed short int|-32,768 ~ 32,767
''|''|unsigned short int|0 ~ 65,535
''| long int|signed long int| -2,1247,483,648 ~ 2,147,483,647
''|''|unsigned long int|0 ~ 4,294,967,295

원래 형태|가장 자주 쓰는 형태
--|--
signed short int|short
unsigned short int|unsigned short
signed long int|int
unsigned long int|unsigned int

## 실수형
실수 자료형|크기|저장할 수 있는 값의 범위
--|--|--
float|4바이트|1.2E-38 ~ 3.4E38
double|8바이트|2.2E-308 ~ 1.8E308

# 상수(constant)
- 프로그램을 실행할 때 한 번 값이 결정되면 프로그램이 끝날 때까지 다른 값으로 바뀌지 않는 정보

### 숫자형 상수
- 가장 기본적인 형태의 상수
- 정수형 상수, 실수형 상수로 나뉜다.

### 문자형 상수
- 작은따옴표를 사용해서 표현한다. 
- 영문자, 숫자형 문자, 특수 문자로 나뉜다.

### 문자열형 상수
- 큰따옴표로 묶어서 표현한다.

# 변수
## 변수 선언
자료형|변수 이름|구분자
--|--|--
signed int|num|;
부호 있는 정수를 저장할 4바이트 메모리를 사용한다는 의미|할당된 메모리 공간의 이름을 num으로 한다는 의미

```c
// 여러개의 변수 선언시 방법
// 1번
int data1;
int data2;
int data3;

//2번
int data1, data2, data3;
```

## 변수의 초기화
- 변수를 사용하기 전에 초기값을 저장하는 과정을 말한다.
- 보통 초기값의 기본은 0으로 한다.
```c
int value;      // 4바이트 크기의 value 변수에 어떤 값이 저장되어 있는지 알 수 없는 상태

int value = 0;  // 4바이트 크기의 value 변수에 정수형 상수 값 0을 넣어 초기화
```

# reference
DO it! C언어 입문 - 김성엽   
동영상 강좌 - 'Do it! C언어 입문' - 3장 ~ 4장   
https://www.youtube.com/watch?v=-JNTP5D8-1A&list=PLiZvlxkcLhakQwbPjkyfuHFy1IVG-VXrP&index=3   
https://www.youtube.com/watch?v=M4I5WUHE_LI&list=PLiZvlxkcLhakQwbPjkyfuHFy1IVG-VXrP&index=4

