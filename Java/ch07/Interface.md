# 인터페이스(interface)
## 인터페이스란
- 추상메서드의 집합이다.

- 구현된 것은 없고, 밑그림만 그려진 기본 설계도이다.
- 인터페이스는 완전히 아무것도 없고, 추상메서드만 갖고 있다. 이때, iv를 가질 수 없다.
- 추상클래스는 인터페이스와 다르게 일반 클래스이면서 단순히 추상메서드를 가지고 있기 때문에 추상클래스가 되는 것이다.

## 인터페이스의 작성
- 인터페이스는 키워드를 class 대신 interface를 사용한다.

- 접근제어자로 public, default를 사용한다.
- 모든 멤버변수는 public static final 이어야 한다.
- 모든 메서드는 public abstract 이어야 한다.
- 인터페이스의 정의된 모든 멤버들은 예외없이 적용되기 때문에 제어자를 생략할 수 있고, 이때 컴파일러가 자동적으로 추가해준다.

```java
interface 인터페이스이름 {
    public static final 타입 상수이름 = 값;     // 상수
    public abstract 메서드이름 (매개변수목록);  // 추상메서드
}
```  
```java
interface PlayingCard{
    public static final int SPADE = 4;
    final int DIAMOND = 3;  // public static final int DIANMOND = 3;
    static int HEART = 2;   // public static final int HEART = 2;
    int CLOVER = 1;         // public static final int CLOVER = 1;

    public abstract String getCardNumber();
    String getCardKind();   // public abstract String getCardNumber();

}
```

## 인터페이스의 상속
- 인터페이스는 인터페이스로부터만 상속받을 수 있다.

- 클래스와 달리 다중상속이 가능하다.
  - 클래스의 경우 다중상속을 하게 되면, 선언부의 이름은 같은데, 구현부에서 내용이 다르기 때문에 충돌이 생겨서 문제가 생긴다. 
 
  - 인터페이스의 경우 구현부가 작성되지 않았기 때문에 다중상속이 가능하다.

- 인터페이스는 클래스와 달리 Object클래스와 같은 최고 조상이 없다.
- 자손 인터페이스는 조상 인터페이스로부터 정의된 멤버를 상속받는다.
  - 자손 인터페이스에서는 정의된 멤버들을 완성시켜야 한다.

## 인터페이스의 구현
- 인터페이스에 정의된 추상메서드를 완성시키는 것이다.
- 'implements'를 사용한다.
- 인터페이스의 메서드 중 일부만 구현한다면, abstract를 붙여서 추상클래스를 선언해야 한다.
```java
class 클래스 이름 implements 인터페이스 이름 {
    // 인터페이스에 정의된 추상메서드를 구현해야 한다.
}

// Fighter클래스는 Fightable를 수현한다라는 의미
class Fighter implements Fightable { 
    public void move (int x, int y) { /*내용생략*/}
    public void attack (Unit u) { /*내용생략*/}
}
```
```java
class Fightable {
    public void move (int x, int y) { /*내용생략*/}
    public void attack (Unit u) { /*내용생략*/}
}

abstract class Fighter implements Fightable { 
    public void move (int x, int y) { /*내용생략*/}
}
abstract class Fighter implements Fightable { 
    public void move (int x, int y) { /*내용생략*/}
    public abstract void attack (Unit u) { /*내용생략*/}
    
```
## 인터페이스를 이용한 다형성
ex)
```java
Fightable f = (Fightable)new Fighter();
or
Fightable f = new Fighter();
```
- Fighter인스턴스를 Fightable타입의 참조변수로 참조하는 것이 가능하다.

- Fightable타입의 참조변수로는 인터페이스 Fightable에 정의된 멤버만 호출가능하다.
- 인터페이스는 메서드의 매개변수 타입으로 사용가능하다. 
- 이때 인터페이스 타입의 매개변수가 갖는 의미란.
  - 메서드 호출 시 해당 인터페이스를 구현한 클래스의 인스턴스를 매개변수로 제공해야 한다.
  - 즉 예제 코드에 의하면 Fightable 인터페이스를 구현한 클래스만 인스턴스가 가능하다는 의미다.
- 매서드의 리턴타입으로 인터페이스의 타입을 지정하는 것이 가능하다.
    ```java
    Fightable method() {
        Fighter f = new Fighter();
        return (Fightable)f;
    }
    ```
    - 호출한 곳은 반환타입과 일치하거나 자동형변화이 가능한 타입이 저장되어야 한다.

## 인터페이스의 장점

### 1. 개발 시간을 단축할 수 있다.<br>
<A와 B를 직접 사용하는 경우><br>
- A가 B를 사용하려면 먼저 B가 완성되어야 A의 코드를 작성할 수 있다.
  
<A가 B를 직접 사용하지 않는 경우>   
- A는 I하고만 관게를 맺는다. 이때 I는 추상메서드 집합
- A는 추상 메서드 호출 가능(이때 추상메서드 본체는 완성되지 않아도 선언은 되었기 때문에 사용가능). 즉 B의 클래스의 코드가 완전히 작성되지 않아도 A 클래스는 코드 작성이 가능하다.
- B는 추상 메서드 본체 완성
- 그래서 개발 시간을 단축할 수 있다.
  
### 2. 변경에 유리한 유연한 설계가 가능하다.

<강한 결합>
```java
// 선언부와 구현부가 같이 있는 클래스
class B {
    public void method() {
        System.out.println("methodInB");
    }
}
```

<느슨한 결합>
```java
// 선언부와 구현부가 분리 - 인터페이스의 장점
interface I {
    public void method();
}

class B implements I {
    public void method() {
        System.out.println("methodInB");
    }
}
```

- 위의 코드보다 더 유연하고, 변경에 유리하다.

- A라는 클래스가 B클래스를 사용할 때 직접 사용하도록 코드를 작성하게 되면 만약 B 대신 C 클래스로 사용이 바뀌게 되면 A도 같이 바꿔야 하는 불편이 존재한다.
- 이때 인터페이스를 사용하면 A라는 클래스는 껍데이기인 인터페이스하고만 관계를 이루기 때문에 알맹이를 바꿔도 문제가 없다.
- 즉, 인터페이스를 사용하면 A라는 클래스는 변경할 필요가 없어진다. 그래서 변경에 유리해진다. 느슨한 결합

<직접적인 관계>
```java
class A { 
    public void methodA(B b) {  // C클래스를 사용하려면 (C b) 수정해야 한다.
        b.methodB();
    }
}

class B {
    public void methodB() {
        System.out.println("methodB()");
    }
}

class InterfaceTest {
    public static void main (string args[]) {
        A a = new A();
        a.methodA(new B()); // B의 객체를 만들어서 넣음, A가 B를 사용(A가 B에 의존)
    }
}
```

<간접적인 관계의 두 클래스>
```java
class A {   // 더 이상 B 클래스와 관계가 없어짐
    public void methodA (I i) {// 인터페이스 I를 구현한 i만 들어오라는 뜻
        i.methodB();
    }
}

// 껍데기(B의 method()를 추상 메서드로 갖는 인터페이스)
interface I { void methodB(); }

// 알맹이(구현)
class B implements I {
    pulic void methodB() {
        System.out.println("methodB()");
    }
}

// B 대신 C로 바꿔도 A는 상관없음
class C implements I {
    public void methodB() {
        System.out.println("methodB() in C");
    }
}

```

### 3. 표준화가 가능하다. (JDBC)

### 4. 서로 관계없는 클래스들을 관계를 맺어줄 수 있다.

## Static 메서드 & 디퐅트 메서드
- JDK1.8부터 디폴트 메서드와 static 메서드를 추가해서 인터프린터에서 사용가능하게 되었다.
  
### 디폴트 메서드
- 인터페이스에 메서드를 추가하는 것은 추상 메서드를 추가한다는 것이다. 그리고 이것은 인터페이스를 구현한 기존의 모든 클래스들이 새로 추가된 메서드를 구현해야 한다는 의미이다. 이때 이것을 해결해주는 것이 디폴트 메서드이다.

- 디폴트 메서드는 키워드 앞에 default를 붙여야 한다.
- 추상 메서드와 몸통{}이 존재한다.
- 접근 제어자는 public이고, 생략가능하다.

### 디폴트 메서드를 사용했을때 문제점
- 여러 인터페이스의 디폴트 메서드 간의 충돌
  - 인터페이스를 구현한 클래스에서 디폴트 메서드를 오버라이딩해야 한다.

- 디폴트 메서드와 조상 클래스의 메서드 간의 충돌
  - 조상 클래스의 메서드가 상속되고, 디폴트 메서드는 생략된다.
  - 즉, 조상 클래스가 우선 순위가 높다.  


# reference
자바의 정석 - 남궁성




