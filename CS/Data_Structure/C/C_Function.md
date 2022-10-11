# 함수
- 정해진 단위 작업을 수행하도록 여러 개의 명령문들을 하나의 그룹으로 묶은 것을 함수라 한다.
- C언어 프로그램은 여러 함수로 이루어져 있다.

## 함수의 정의
```C
int Sum(int value1, int value2)
{
    int result = value1 + value2;
    return result;
}
```
함수 이름|매개변수|작업내용|반환값|반환형
--|--|--|--|--
int|Sum|(int value1, int value2)|return result|int


### 매개변수
- 호출자에서 전달하는 값을 피호출자에서 전달 바는 역할을 하는 변수를 의미한다.
- 함수 안에서 선언한 변수들은 해당 함수에서만 사용 가능하다.

### 반환값
- 함수에서 return이라는 예약어를 사용하면 함수는 그 위치에서 종결한다.
- return 뒤에 명시된 result 변수 값이 Sum 함수의 반환 값이 된다.

## 함수의 호출 과정
```c
int Sum(int value1, int value2) 
{
    int result = value1 + value2;   
    return result;
}

void main()
{
    int a = 2, b = 3, value;
    value = Sum(a,b);   
}   
```

```c
Sum(a,b);   // 1. main 함수가 Sum 함수를 호출하고, 이때 a, b 값을 Sum 함수에 전달

Sum(int value1, int value2) // 2. SUm 함수의 매개변수에 main 함수에서 전달 받은 값이 복사된다

int result = value1 + value2;  // 3. 입력된 값으로 더하기 작업을 수행

return result;         // 4. Sum 함수는 int 형으로 결과 값을 반환

value = Sum(a,b);          // 5. SUm 함수의 반환값을 int형 변수 value에 저장
```

## main 함수 정리
- C언어 프로그램은 main 함수가 시작점이다.
```c
// main 함수의 반환값
// 1. 반환이 필요한 경우 - int형으로 반환
int main()
{
    return 1;
}
/*
프로그램이 정상적으로 끝나면 1 값을 반환한다는 의미
*/

// 2. 반환이 필요 없는 경우 - void형으로 반환
void main()
{
    // 반환값x
}
```

## 함수선언
- 컴파일러는 코드를 위에서 아래로 읽기 때문에 호출자가 피호출자보다 위에 있는 경우에 오류가 발생한다.
- 이때 오류를 방지하기 위해 함수만 함수 원형(함수 이름, 매개변수, 반환 자료형을 포함한 표현식)을 위에 선언한다.
```c
int Sum(int value1, int value2);    // 함수 선언

void main()
{
    int s;
    s = Sum(2,3);
}

int Sum(int value1, int value2)
{
    int result = value1 + value2;
    return result;
}
```

# reference
DO it! C언어 입문 - 김성엽   
동영상 강좌 - 'Do it! C언어 입문' - 5장   
https://www.youtube.com/watch?v=Twd5C84EI7U&list=PLiZvlxkcLhakQwbPjkyfuHFy1IVG-VXrP&index=5
  
