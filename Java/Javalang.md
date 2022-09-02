# Object클래스
- 모든 클래스의 최고 조상. 오직 11개의 메서드만을 가지고 있다.
- notify(), wait() 등은 쓰레드와 관련되 메서드이다.


## equals(Object obj)
- 객체 자신(this)과 주어진 객체(obj)를 비교하고, 같으면 true 다르면 false를 알려준다.
- Object클래스의 equal()는 객체의 주소를 비교(참조변수 값 비교), 주소가 같을 때만 참이다.
- 인스턴스 변수(iv)의 값을 비교하려면 equals()를 오버라이딩해야 한다.

```java
class Value {
    int value;

    Value(int value) {
        this.value = value;
    }
}

class EqualEx {
    public static void main(String[] args) {
        // 서로 다른 두 객체는 다른 주소를 가지고 있다.
        Value v1 = new Value(10);
        Value v2 = new Value(10);

        // v1은 this, v2가 obj
        System.out.println(v1.equals(v2));
    }
}
```
```java
    // 오버라이딩 해서 주소가 아닌 값으로 참 또는 거짓을 구별하게 한다.
    // obj에는 값이 없기 때문에 형변환을 해서 값이 있게 해야 한다.
    public boolean equals(Object obj) {
        //return this == obj;   // 원래의 상태, 서로 다른 객체는 항상 거짓.

        // 참조변수의 형변환 전에는 항상 instanceof로 확인해야 한다. 
        if (!(obj instanceof Value)) return false;

        Value v = (Value)obj;   // Value 클래스에서는 vale라는 iv가 존재하지만 , obj에는 존재하지 않기 때문에 형변환시켜서 사용할 수 있게 한다.

        return this.valu == obj.value;
    }
```

## hashCode()
- 객체의 해시코드(hash code)를 반환하는 메서드
- Object클래스의 hashCode()는 객체의 주소를 int로 변환해서 반환한다. 그래서 객체마다 다른 값을 가진다.
- 객체의 지문이라고 한다.
- equal()가 iv를 활용할 수 있게 오버라이딩하면, hashCode()도 iv를 활용할 수 있게 오버라이딩해야 한다.
- equal()의 결과가 true인 두 객체의 해시코드는 같아야 한다.
- 64bit JVM에서는 주소값이 8byte이기 때문에 해시코드를 만들때 해시코드가 중복될 수 있다.
- System.identityHashCode(Object obj)는 onject클래스의 hashCode()와 동일, 이때 호출결과는 실행 할 때마다 달라진다.
```java
String str1 = new String("abc");    // 아래와 같이 같다면
String str2 = new String("abc");    
System.out.println(str1.equals(str2));  // True
System.out.println(str1.hashCode());    // 9997 
System.out.println(str2.hashCode());    // 9997
``` 
```java
pulic class objcect {
    ...
    public native int hasCode();
}
//native는 네이티브 메서드(OS의 메서드)를 지칭한다. 그래서 불러오기 때문에 내용없이 사용가능하다.
```

## toString()
- 객체를 문자열(String)으로 변환하기 위한 메서드
- iv를 활용할 수 있도록 오버라이딩한 메서드를 더 사용한다.
- 객체는 iv집합이므로, 객체를 문자열로 변환한다는 것을 iv의 값을 문자열로 변환한다는 것을 의미한다.
  ```java
  public String toString() {
    return getClass().getName() + "@" + Integer.toHexString(hasCode());
  }
  ```


# reference
자바의 정석 - 남궁성
