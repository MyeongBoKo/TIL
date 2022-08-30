# 예외처리(exception handling)
 
## 프로그램 오류
1. 컴파일 에러(compile-time error): 컴파일 할 때 발생하는 에러
   - 컴파일 에러가 발생하면 오류를 수정하기 전까지 프로그램을 만들 수 없어서 프로그램을 실행할 수 없다.
   - 컴파일러이란
     - 구문체크
     - 번역
     - 최적화(소스코드의 최적화)
     - 생략된 코드 추가 (ex: extends Object)
    
2. 런타임 에러(runtime error): 실행 할 때 발생하는 에러
   - 실행은 할 수 있지만 프로그램이 실행을 하다가 종료된다.
   - java의 런타임 에러
     - 에러: 프로그램 코드에 의해서 수습될 수 없는 심각한 오류
       - ex) OOME(Out of Memory Error)
     - 예외: 프로그램 코드에 의해서 수습될 수 있는 다소 미약한 오류, 예외는 2가지로 나뉜다.
       - Exception과 그 자손
       - RuntimeExceptoin과 그 자손
   - 에러는 처리할 수 없지만 예외는 처리해보자
   
3. 논리적 에러(logical error): 작성 의도와 다르게 동작
    - 프로그램이 동작은 하지만 내가 원하는 의도대로 작동하지 않는다.
  
## 예외 클래스의 계층구조
- 계층구조는 Exception클래스와 그 자손들, RuntimeException클래스와 그 자손들로 나뉜다.

- Exception 클래스와 그 자손들의 경우 사용자의 실수와 같은 외적인 요인에 의해 발생하는 예외
- RuntimeException클래스와 그 자손들의 경우 프로그래머의 실수로 발생하는 예외
----
- Exception
  - IoException : 입출력 예외 - 외적인 요인
  
  - ClassNotFoundException : 클래스가 존재X - 외적인 요인
  - ...
---------------  
  - RuntimeExcetpion
    - ArithmeticException : 산술계산예외
    - classCastException  : 형변환  
    - NullPointerException : null인 객체에서 값을 불러올때 발생하는 에러
    - ...
    - IndexOutOfBoundsException : 배열 범위 벗어남
---  

 
## 예외처리하기 try-catch문

### 예외처리란
- 프로그램 실해 시 발생할 수 있는 예외의 발생에 대비한 코드를 작성하는 것

- 프로그램의 비정상 종료를 막고, 정상적인 실행상태를 유지하는 것 

<예외의 발생과 catch블럭><br>
- 예외가 발생하면, 이를 처리할 catch블럭을 찾아 내려감

- 일치하는 catch블럭이 없으면, 예외는 처리 안됨
- Exception이 선언된 catch블럭은 모든 예외 처리(마지막 catch블럭)
- if문과 달리, try블럭이나 catch블럭 내에 포함된 문장이 하나뿐이어도 괄호{}를 생략할 수 없다.

```java
try {
    // 예외가 발생할 가능성이 있는 문장들을 넣는다.
} catch (Exceptional1 e1) {
    // Exceptional1이 발생했을 경우, 이를 처리하기 위한 문장을 적는다.
} catch (Exceptional2 e2) {
    // Exceptional2이 발생했을 경우, 이를 처리하기 위한 문장을 적는다.
} catch (ExceptionalN eN) {
    // ExceptionalN이 발생했을 경우, 이를 처리하기 위한 문장을 적는다.
}
```
## try-catch문의 흐름
- try블럭 내에서 예외가 발생하는 경우
  - 발생한 예외와 일치하는 catch블럭이 있는지 확인한다.
  
  - 일치하는 catch블럭을 찾게 되면, 그 catch블럭 냉의 문장들을 수행하고, 전체 try-catch문을 빠져나가서 그 다음 문장을 계속해서 수행한다. 
  - 만일 일치하는 catch블럭을 찾지 못하면, 예외는 처리되지 못한다. 그러면 프로그램이 비정상적으로 종료된다.

## 예외의 발생과 catch블럭
- 발생한 예외에 해당하는 클래스의 인스턴스가 만들어진다.
- Exception클래스는 모든 예외 클래스의 조상이기 때문에 catch블럭 내에 Exception클래스 타입의 참조변수를 선언하면 어떤 종류의 예외도 처리된다.

## printStackTrace() & getMessage()
- printStackTrace(): 
  >예외발생 당시의 호출스택(Call Stack)에 있었던 메서드의 정보와 예외 메시지를 화면에 출력한다.
- getMessage()
  >발생한 예외클래스의 인스턴스에 저장된 메시지를 얻을 수 있다.

## 멀티 catch블럭
- 내용이 같은 catch 블럭을 하나로 합친 것
- 여러 catch 블럭을 '|' 기호를 이용해서 하나로 묶는다.
- 연결된 클래스는 부모와 자식의 관계가 될 수 없다.(만약 부모와 자식관계면 굳이 두개를 작성할 필요가 없다.)
- 메서드 사용 시 공통된 메서드를 사용해야 한다. 그렇지 않으면 컴파일러가 누구의 메서드인지 몰라서 에러를 발생시킨다.

## 예외 발생시키기
1. 연산자 new를 이용해서 발생시키려는 예외 클래스의 객체를 만든다.   
`Exception e = new Exception("고의로 발생시켰음");`

2. 키워드 throw를 이용해서 예외를 발생시킨다.   
`throw e;`

## checked예외 & unchedcked예외
- checked예외: **컴파일러**가 예외 처리 여부를 체크(에외 처리 필수)
  - Exception과 자손
  - try-catch 필수
- unchecked예외: **컴파일러**가 예외 처리 여부를 체크 안함(예외 처리 선택)
  - RuntimeException과 자손 
  - try-cath 선택

## 메서드에 예외 선언하기
- 예외를 처리하는 방법: try-catch문, 예외 선언하기, 은폐(빈 catch블럭)

### 예외 선언하기
- 메서드가 호출시 발생가능한 예외를 호출하는 쪽에 알리는 것
- 예외를 발생시키는 키워드 **throw**와 예외를 메서드에 선언할 때 쓰이는 키워드 **throws**
- Exception클래스 및 자손 클래스는 예외 처리가 필수이기 때문에 선언을 해야한다.
- 이때 RuntimeException클래스 및 자손 클래스는 예외 처리가 선택이기 때문에 선언을 하거나 혹은 하지 않아도 된다.
- 선언은 필수처리만 적는 것이 정석이다.
  
```java
// method()를 호출하면 이런 예외들이 발생할 수 있다는 것을 알려주는 것.
void method() throws Exception1, Exception2, Exception3, ... ExceptionN {
    // 메서드의 내용
}
```
```java
void method() throws Exception {
    // 메서드의 내용
}
// Exception은 모든 예외의 조상(즉, 모든 종류 예외가 발생가능)
```
<``오버라이딩``-참고>   
1. 선언부 일치
2. 접근제어자보다 좁게 설정하면 안된다.
3. 조상보다 많은 예외를 선언하면 안된다.
   
```java
// startInstall() 메서드들 사용하면 두가지 예외가 발생할 수 있다는 것을 알리는 것

static void strartInstall() throws SpaceException, MemoryException {
    if(!enoughSpace()) {    // 충분한 설치 공간이 없으면...
        throws new SpaceException("설치할 공간이 부족합니다.");
    }
    if(!enoughMemory()) {   // 충분한 메모리가 없으면...
        throw new MemoryException("메모리가 부족합니다.");
    }
}   // staticInstall메서드의 끝
```



## finally블럭
- finally 블럭은 예외의 발생 여부에 상관없이 실행되어야할 코드를 포함시킬 목적으로 사용된다.
- 코드 중복을 막기 위해 사용된다.
  ```java
  try {
    // 예외가 발생할 가능성이 있는 문장들을 넣는다.
  } catch (Exception1 e1) {
    // 예외처리를 위한 문장을 집어넣는다.
  } finally {
    // 예외의 발생여부에 관계없이 항상 수행되어야하는 문장들을 넣는다.
    // finally블럭은 try-catch문의 맨 마지막에 위치해야 한다.
  }
    
  ```
## 사용자정의 예외 만들기
1. 조상선택(Exception or RuntimeException)
2. String 매개변수가 있는 생성자를 집어넣는다.

```java
class MyException extends Exception {
    MyException(String msg) {// 문자열을 매개변수로 받는 생성자
        super(msg);}    // 조상인 Exception클래스의 생성자를 호출한다.
}
```

## 예외 되던지기(exception re-throwing)
- 예외를 처리한 후에 다시 예외를 발생시키는 것
- 호출한 메서드와 호출된 메서드 양쪽 모두에서 예외처리하는 것
- 예외처리를 2번의 과정을 거친다.

## 연결된 예외(chained exception)
- 한 예외가 다른 예외를 발생시킬 수 있다.

```java
public class Throwable implements Serializable {
    ...
    private Throwable cause = this; // 객체 자신(this)을 원인 예외로 등록
    ...
    public synchronized Throwable initCause(Throwable cause) {  // 예외 A를 매개변수로 지정
        ...
        this.cause = cause; // 지정해준 A를 iv에 저장
        return this;
    }
}
// 예외 안에 또 다른 예외를 포함시키는 것을 연결된 예외이다.

```

```java
void install() throws InstallException {    
    try {
        startInstall();         // SpaceException 발생(저장공간부족)
        copyFiles();
    } catch (SpaceException e)  { 예외A인 e
        InstallException ie = new InstallException("설치중 예외발생");  // 예외 생성, 예외B인 ie, 이때 A를 B에 원인예외로 등록
        ie.initCause(e);    // InstallException의 원인 예외를 SpaceException으로 지정, 예외 A
        throw ie;           // InstallException을 발생시킨다. 예외 B 
    } catch (MemoryException me)    {
        ...
    }

}
```
### 연결된 예외 이유
1. 여러 예외를 하나로 묶어서 다루기 위해서
    - 프로그램을 작성하다 보면 catch를 많이 작성하게 되는데 이것을 하나의 catch 블럭으로 만들기 위해서 연결된 예외를 사용한다. 이때 위의 코드처럼 install() 안으로 집어넣었다.
     1. installException을 만들고, 
     2. 이 안에 실제 예외를 집어넣는다. 
     3. 이 예외를 던진다. 
     4. 호출한 쪽에서는 installException만 적으면 된다.

2. checked예외를 unchecked예외로 변경하려 할 때
   - 필수처리를 선택처리로 바꿀때 사용
   ```java
   static void startInstall() throws SpaceException, MemoryException {
    if(!enoughSpace())              // 충분한 설치 공간이 없으면....
        throw new SpaceException("설치할 공간이 부족합니다.");

    if(!enoughMemory())             // 충분한 메모리가 없으면...
        throw new MemoryException("메모리가 부족합니다.");
   }
   ```   

   ```java
   static void startInstall() throws SpaceException {
    if(!enoughSpace())              // 충분한 설치 공간이 없으면....
        throw new SpaceException("설치할 공간이 부족합니다.");

    if(!enoughMemory())             // 충분한 메모리가 없으면...
        throw new RunTimeException(new MemoryException("메모리가 부족합니다."));
    }
    // RunTimeException의 생성자를 이용했다.
   ```

    
