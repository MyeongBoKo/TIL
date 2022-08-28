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

# reference
자바의 정석 - 남궁성
