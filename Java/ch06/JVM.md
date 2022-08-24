

# JVM의 메모리 구조
## 호출스택(call stack)
- 호출스택은 메서드의 작업에 필요한 메모리 공간을 제공한다.

- 메서드가 호출되면, 호출스택에 호출된 메서드를 위한 메모리가 할당된다.
- 이 메모리는 메서드가 작업을 수행하는 동안 지역변수(매개변수 포함)들과 연산의 중간 결과 등을 저장하는데 사용한다.
- 메서드가 작업을 마치면 할당되었던 메모리공간은 반환되어 비어진다.
  
|호출스택 특징|
|--|
|메서드가 호출되면수행에 필요한 만큼의메모리를 스택에 할당받는다.|
|메서드가 수행을 마치고나면 사용했던 메모리를 반환하고 스택에서 제거된다.|
|호출스택의 제일 위에 잇는 메서드가 현재 실행 중인 메서드이다.|
|아래에 있는 메서드가 바로 위의 메서드를 호출한 메서드이다.|

기본형 매개변수 - 변수의 값을 읽기만 가능한다.<br>
참조형 매개변수 - 변수의 값을 읽고 변경할 수 있다.<br>

### 기본형 매개변수 예제
```java
class Data {int x}

class PrimitiveParamEx {
    public static main(String[] args) {
        Data d = new Data();
        d.x = 10;
        System.out.println("main() : x =" + d.x);

        change(d.x);
        System.out.println("After change(d.x)");
        System.out.println("main() x = "+ d.x);
    }

    static void change (int x) {
        x = 1000;
        System.out.println("change() : x = " + x);
    }
}

/*
main() : x = 10
After change(d.x)
main() : x = 10
change() : x = 1000
/*
```
```
1. change메서드가 호출되면서 d.x가 change 메서드의 매개변수 x에 복사된다.
2. change메서드에서 x의 값이 1000으로 변경
3. change메서드가 종료되면서 매개변수 x는 스택에서 삭제된다.
```

### 참조형 매개변수 예제
```java
class Data {int x}

class ReferenceParamEx {
    public static main(String[] args) {
        Data d = new Data();
        d.x = 10;
        System.out.println("main() : x =" + d.x);

        change(d);
        System.out.println("After change(d)");
        System.out.println("main() x = "+ d.x);
    }

    static void change (Data D) {
        d.x = 1000;
        System.out.println("change() : x = " + x);
    }
}

/*
main() : x = 10
After change(d.x)
main() : x = 1000
change() : x = 1000
/*
```
```
1. change메서드가 호출되면서 참조변수 d의 값(주소)이 매개변수 d에 복사된다.
그래서 매개변수 d에 저장된 주소값을 통해서 x에 접근이 가능하다.
2. change메서드에서 매개변수 d로 x의 값을 1000으로 변경한다.
3. change메서드가 종료되면서 매개변수 d는 스택에서 삭제된다.
```
### 참조형 반환타입 예제
```java
class Data {int x}

class ReferenceReturnEx {
    public static main(String[] args) {
        Data d = new Data();
        d.x = 10;
        System.out.println("main() : x =" + d.x);

        Data d2 = copy(d);
        System.out.println("d.x ="+d.x);
        System.out.println("d2.x ="+d2.x);
    }

    static Data copy (Data D) {
        Data tmp = new Data();
        tmp.x = d.x

        return tmp;
    }
}

/*
d.x = 10
d2.x = 10
/*
```
```
1. copy메서드를 호출하면서 참조변수 d의 값이 매개변수 d에 복사된다.
2. 새로운 객체를 생성한 다음, d.x에 저장된 값을 tmp.x에 복사한다.
3. copy메서드가 종료되면서 반환한 tmp의 값은 참조변수 d2에 저장된다.
4. copy메서드가 종료되어 tmp가 사라지지만, d2로 새로운 객체를 다룰 수 있다.
```
#### 반환타입이 **참조형**이라는 것은 메서드가 **객체의 주소**를 반환한다는 것을 의미한다.

# Reference
자바의 정석 - 남궁성
