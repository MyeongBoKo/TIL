# 오버로딩
## 오버로딩이란
- 한 클래스 내에 같은 이름의 메서드를 여러 개 정의하는 것을 메서드 오버로딩
  또는 간단하게 오버로딩이라고 한다.
- 하나의 멧서드 이름에 하나의 기능만 구현해야 하는데, 하나의 메서드 이름으로 여러 기능을 구현하기 때문에 오버로딩이라고 한다.


## 오버로딩 조건
- 메서드의 이름이 같아야 한다.
- 매개변수의 개수 또는 타입이 달라야 한다.
- 반환 타입은 영향을 주지 않는다.

### 오버로딩의 잘못된 경우
1. 매개변수의 개수 또는 타입이 같아서 오버로딩이 될 수 없는 경우
```java
int add(int a, int b) {return a + b; }
int add(int x, int y) {return x + y; }
```

2. 반환 타입을 제외하고, 나머지 조건을 만족하지 않아서 오버로딩이 될 수 없는 경우
```java
int add(int a, int b) {return a + b; }
long add(int a, int b) {return (long) a + b; }
 ```
 

3. 조건을 만족하기 때문에 오버로딩이지만, 조건에 따라 오버로딩이 될 수 없는 경우
```java
long add (int a, long b) {return a + b; }
long add (long a, int b) {return a + b; }
```
- add(3, 3L) 또는 add(3L, 3)은 호출가능하지만, add(3,3)은 호출이 불가능하다. 어느 메서드를 사용해야 할지 컴파일러가 알 수 없기 때문에 컴파일 에러가 발생한다.

### 오버로딩이 잘된 경우
```java
int add(int a, int b) {return a + b; }
long add(long a, long b) {return a + b; }
long add(int [] a) {		// 배열의 모든 요소의 합을 반환한다.
   	long result = 0;
   		
   	for(int i = 0; i < a.length; i++) {
   			result += a[i];
   	}
   	return result;
}
```

## 오버로딩의 장점
- 오버로딩을 사용함으로써 오류의 가능성을 줄여준다.
- 메서드의 이름을 보고 어떤 기능인지 쉽게 유추 가능하다.
- 메서드의 이름을 절약해서, 시간적인 장점을 준다.



# Reference
자바의 정석 - 남궁성
