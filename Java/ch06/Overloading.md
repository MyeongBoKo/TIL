

# 오버로딩
## 오버로딩이란
- 한 클래스 내에 같은 이름의 메서드를 여러 개 정의하는 것을 메서드 오버라이딩 
  또는 간단하게 오버라이딩이라고 한다.


## 오버라이딩 조건
- 메서드 이름이 같아야 한다.

- 매개변수의 개수 또는 타입이 달라야 한다.

- 반환 타입은 영향을 주지 않는다.

```java
int add(int a, int b) {return a + b; }
int add(int x, int y) {return x + y; }
```
```
매개변수의 이름만 같지 매개변수 타입이 같기 때문에 오버로딩이 아닌 코드 중복이다.
```
  
```java
int add(int a, int b) {return a + b; }
long add(int a, int b) {return (long) a + b; }
 ```
 
```
반환값만 다를뿐 나머지는 같기 때문에 오버로딩이 아니다.
```

  
```java
long add (int a, long b) {return a + b; }
long add (long a, int b) {return a + b; }
```

```
오버로딩이지만 단순히 매개변수의 순서를 바꾸었기 때문에 호출시에 어느 것을 호출해야 할지 모를때 에러가 발생할 수 있다.
```

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

```
위의 코드는 오버로딩의 적절한 예이다.
```

# Reference
자바의 정석 - 남궁성
