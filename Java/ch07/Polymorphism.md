# 다형성(polymorphism)
## 다형성이란
- 사전적 의미로 여러 가지 형태를 가질 수 있는 능력을 의미한다.

- 조상클래스 타입의 참조변수로 자손클래스의 인스턴스를 참조할 수 있도록 하는 능력을 의미한다.
- **자손타입의 참조변수로 조상타입의 인스턴스를 참조할 수 없다.**

```java
class Parent {
    ...
}

class Child extends Parent {
    void mathed();
}
```  
```java
Parent p = new Parent();


Child c = new Child();
```
인스턴스를 생성하기 위해서 각 타입에 맞는 참조변수를 사용해서 생성시켰다. 하지만 다형성을 이용해서 타입이 맞지 않는 참조변수를 통해 인스턴스 생성이 가능하다.

```java
Parent p = new Child(); // 가능 , Parent class에 있는 맴버의 개수

Child c = new Child(); // 가능, Parent class + Child class의 맴버의 개수

Child c = new Parent(); // 불가능
```
- 조상 클래스 타입의 참조변수를 통해 인스턴스를 생성하게 되면 조상 클래스에 있는 맴버만 접근가능하다.

- 자손타입의 참조변수로 조상타입의 인스턴스를 접근할 수 없다. child의 인스턴스의 맴버의 개수가 P의 참조변수로 접근할 수 있는 기능보다 많기 때문이다.
  
## 참조변수의 형변환
- 참조변수의 형변환에서 가장 중요한 것은 사용할 수 있는 맴버의 개수를 조절한다는 것이다.

- 맴버의 개수만 바뀔뿐 객체 및 주소는 바뀌지 않는다.

```java
class Car{
    ...
}

class FireCar extends Car {
    void method();    
    ...
}


class Amnulance extends Car {
    void method1();
    ...
}

// 형변환 하는 방법
//조상 <- 자손
Car c = (Car)fc;                // (Car) 생략가능

// 조상 -> 자손
FireCar fc = (FireCar)c;        // (FireCar) 생략가능

// 형변환 하지 못하는 경우
FireCar fc = (FireCar)a;        // 상속관계가 아닌 클래스간의 형변환 불가
Amnulance a = (Amnulance)fc;    // 상속관계가 아닌 클래스간의 형변환 불가

```  
- 참조변수가 가리키는 인스턴스의 타입이 무엇인지 확인하는 것이 중요하다.
  
## instanceof연산자
- 참조변수의 형변환 가능여부를 확인해 주는 연산자이다.

- 검사한 타입의 연산결과가 True로 반환되면 형변환이 가능하다.
- Object 타입은 모든 class의 조상이기 때문에 Object 타입으로 형변환이 가능하다.

### 형변환 순서
1. instanceof연산자를 이용해서 True 또는 false의 값을 받는다.
2. True이면 형변환을 할 수 있기 때문에 형변환을 진행한다. 
이때 false 이면 형변환이 불가하다. 

## 다형성이 가지는 장점
### 매개변수의 다형성
- 참조형 매개변수는 메서드를 호출시, 자신과 같은 타입 또는 자손타입의 인스턴스를 넘겨줄 수 있다.
  
- 다형성을 이용하지 않는다면 코드를 작성할때 같은 메서드를 처리하기 위해 코드가 복잡해지는데, 다형성을 이용하면 하나의 메서드로 간단히 처리가 가능하다.
  
```java
class Product {
    int price;
    int bonusPoint;
}

class Tv extends Product{}
class Computer extends Product{}
class Audio extends Product{}

class Buyer {
    int money = 1000;
    int bonusPoint = 0;

    // 다형성을 이용하지 않고 코드를 작성할 경우
    void buy(Tv t) {
        money = money = t.price;
        bonusPoint = bonusPoint + t.bonusPoint;
    }
    void buy(Computer c) {
        money = money = c.price;
        bonusPoint = bonusPoint + c.bonusPoint;
    }
        
    void buy(Audio a) {
        money = money = a.price;
        bonusPoint = bonusPoint + a.bonusPoint;}
}
```
```java
 // 다형성을 이용해서 코드를 작성하는 경우
    void buy(product p){
        money = money - p.price;
        bonusPoint = bonusPoint + p.bonusPoint;
    }

    // 이때 p는 상황에 따라서 
    new Tv();
    new Computer();
```
### 여러 종류의 객체를 배열로 다루기
- 조상타입의 참조변수 배열을 사용하면, 공통의 조상을 가진 서로 다른 종류의 객체를 배열로 묶어서 다룰 수 있다.

- 묶어서 다루고 싶은 객체들의 상속관계를 따져서 가장 가까운 공통조상 클래스 타입의 참조변수 배열을 생성해서 객체들을 저장하면 된다. 
  
#### Vector클래스 사용
- Vector는 가변배열

- Vector클래스는 내부적으로 Object타입의 배열을 가지고 있다. 그래서 모든 종류의 객체를 저장할 수 있다.
-  배열의 크기를 알아서 관리해주기 때문에 저장할 인스턴스의 개수에 신경쓰지 않아도 된다.

# reference
자바의 정석 - 남궁성
