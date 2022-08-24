

# 객체 배열(= 참조 변수 배열)
- 많은 수의 객체를 배열을 통해서 다룰 수 있는데, 이때를 *객체 배열*이라고 한다. 객체 배열안에 객체가 저장되는 것이 아니고, 객체의 주소가 저장된다. 그리고 객체 배열은 참조변수들을 하나로 묶은 *참조 변수 배열*이다.

# 객체 배열 생성 및 실행
```java
Code c1, c2, c3; -> Code[] codeArr = new Code[3];
``` 
- Code 타입의 참조변수가 3개로 이루어진 객체 배열
- 참조 변수들이 만들어진 것이지, 객체가 저장되지 않은 상태이다.
  
```java
codeArr[0] = new Code();
codeArr[1] = new Code();
codeArr[2] = new Code();
 ```
 - 객체를 생성해서 배열의 각 요소에 저장한다.
 ```java
 codeArr[] = { new Code(), new Code(), new Code() };
 ```
 - 배열의 초기화를 이요해서 간단하게 한 줄로 표현한다.
  
  ```java
  Code[] codeArr = new Code[50];   // 배열의 길이가 50
  
  for (int i = 0; i < codeArr.length; i++>) {
    codeArr[i] = new Code();
  }
  ```
  - 객체가 너무 많아서 직접 작성하기 어려울때, 반복문을 이용해서 표현할 수 있다.
