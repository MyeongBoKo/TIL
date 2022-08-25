# 상속(inheritance)
## 상속이란
- 기존의 클래스를 재사용하여 새로운 클래스를 작성하는 것이다.

- 두 클래스를 부모와 자식의 관계로 맺어주는 것을 말한다.
  
### 상속을 구현하는 방법
- 작성하려는 새로운 클래스의 이름 뒤에 extends와 함께 기존의 클래스 이름을 작성하면 된다.
  ex)
    ```java
    class Child extends Parent {
        // ...
    }
    ```
### 조상 클래스&자손 클래스
조상 클래스 | 부모(parent)클래스, 상위(super)클래스, 기반(base)클래스
--|--
자손 클래스 | 자식(child)클래스, 하위(sub)클래스, 파생된(derived) 클래스

- 생성자와 초기화 블럭은 상속되지 않는다. 맴버만 상속된다.
  
- 자손 클래스는 조상 클래스의 모든 맴버를 상속받기 때문에 자손 맴버의 개수가 조상 맴버의 개수보다 같거나 크다.
  
  
  ex)
  ```java
  class Parent{
    int age;                        // 조상 맴버
  }

  class Chile extends Parent{
    void play() {                   // 자손 맴버
        System.out.println("놀자~");
    }
  }
  ```

클래스 | 클래스의 맴버
:--:|:--
Parent| age
Child | age, play()

### 상속 받아서 작성된 클래스&상속 받지 않고 작성된 클래스 
```java
// 상속 받지 않고 작성된 클래스
class Point3D {
    int x;
    int y;
    int z;
}
```
- Point 관계가 없다.
- Point class의 영향을 받지 않는다.
- 객체생성은 같게 생성된다.
  
```java
  // 상속 받아서 작성된 클래스
  class Point {
    int x;
    int y;
  }

  class Point3D extends Point {
    Poin3D p = new Point3D();
    int z;
  }
 ```
- Point 관계가 있다.
- Point class의 영향을 받는다.
- 객체생성은 같게 생성된다.

# 포함
## 포함이란
- 클래스의 맴버변수로 다른 클래스 타입의 참조변수를 선언하는 것을 말한다.
```java
class Point {
    int x;
    int y;
}

class Circle {
    Point p // = new Point();
    int r;

    Circle() {
        p = new Point();
    }
}
```
# 상속&포함의 관계
상속관계|'~은 ~이다.(is - a)'
--|--
포함관계|'~은 ~이다.(has - a)'
- 포함이 대부분 많이 사용된다. 
- 상속의 경우 조건이 타기 때문에 꼭 필요한 경우에 사용된다.

# 단일 상속
- 자바에서는 오직 단일 상속만을 허용한다.

- 다중상속을 사용하지 않기 때문에 클래스 간의 관계가 보다 명확해지고 코드를 신뢰할 수 있게 한다.
- 다중상속처럼 표현하고 싶다면 비중 높은 클래스 하나만 상속하고 나머지는 포함의 관계를 통해서 표현한다.
  
```java
class TVVR extends Tv, VR { // 에러가 발생한다. 조상은 하나만 허용된다.
    // ...
}
```

# 모든 클래스의 조상(Object클래스)
- Object클래스는 모든 클래스 상속계층도의 최상위에 있는 클래스이다.

- 다른 클래스로부터 상속 받지 않는 모든 클래스들은 자동적으로 Object클래스로부터 상속받게 한다.
- 만약 사용자가 클래스가 Object클래스로부터 상속받는 코드를 작성하지 않는다면 컴파일러가 자동으로 'extends Object'를 추가한다.
- Object클래스를 상속받기 때문에 Object클래스에 있는 11개의 메서드를 사용할 수 있다. ex) toString(), equal(), hasCode(), .... 

```java
class Tv{
    ...
}

class Tv extends Object {
    ...
}
```

# reference
자바의 정석 - 남궁선



