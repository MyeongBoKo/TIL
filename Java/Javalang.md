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
## String 클래스
- 문자열을 다루기 위한 클래스
- String클래스 = 데이터(char[])+메서드(문자열 관련)
- 내용을 변경할 수 없는 불변(immutable)클래스
- 덧셈 연산자를 이용한 문자열 결합은 성능이 떨어진다.(연산을 할 때 마다 새로운 객체를 생성하기 때문)
- 이때 문자열 결합이나 변경이 잦다면, 내용을 변경가능한 StringBuffer를 사용해야 한다.
  ```java
  String a = "a";
  String b = "b";
  System.out.println(a); // a

  a = a + b;
  
  System.out.println(a); // ab
  ```
  a의 값이 "ab"로 바뀐 것 처럼보이지만, 실제로는 a라는 참조변수가 "a"를 가리키고, b라는 참조변수가 "b"를 가리키는데 이때 더하면 "ab"가 생기는데 이때 객체가 새로 생성된다. 이 새로 생긴 객체의 주소가 a에 복사되고 난 후, a는 전에 연결된 "a"의 관계가 끓어지고, 새로 만들어진 "ab"를 가리키게 된다.

## 문자열의 비교
### *String str = "abc"* & *String str = new String("abc");*

- 문자열 리터럴로 만들면 하나의 문자열을 여러 참조변수가 공유한다.
- new연산자를 이용하면 항상 새로운 문자열이 만들어진다.
- 문자열의 내용은 변경 불가이기 때문에 여러 참조변수가 공유해도 문제가 되지 않기 때문에 굳이 새로운 문자열을 만드는 방식을 사용할 필요가 없어진다.
- 문자열 비교 대입문자를 사용할 때 ==(주소비교) 사용하면 안된다. 
- 비교시 equals()메서드(내용비교)를 사용해야 한다.

### 문자열 리터럴
- 문자열 리터럴은 프로그램 실행시 자동으로 생성된다. constant pool에 저장된다.
- 같은 내용의 문자열 리터럴은 하나만 만들어진다. 그리고 공유를 한다.
  
## 빈 문자열("", empty string)
- 내용이 없는 문자열, 크기가 0인 char형 배열을 저장하는 문자열   
  `String str = ""; // str을 빈 문자열로 초기화 ` 
- 크기가 0인 배열을 생성하는 것은 어느 타입이나 가능
  `char[] chArr = new char[0]; // 길이가 0인 char 배열`
  `int[] iArr = {};            // 길이가 0인 int 배열`

- 문자와 문자열의 초기화
  ```java
  String s = "";    // 빈 문자열로 초기화
  char c = ' ';     // 공백으로 초기화
  ```

## 문자열과 기본형 간의 변환
### 숫자를 문자열로 바꾸는 방법
```java
int i = 100;    
String str1 = i +"";                // 100을 "100"으로 변환 방법 1
                                    // 숫자 + ""(빈문자열) -> 문자열
String str2 = String.valueOf(i);    // 100을 "100"으로 변환
                                    // 메서드 사용, 속도가 빠름
```

### 문자열을 숫자로 바꾸는 방법
```java
int i = Integer.parseInt("100");     // "100"을 100으로 변환하는 방법1
                                     // 문자열을 숫자열로 바꿔주는 메서드   
                                     // 올드한 방법

int i2 = Integer.valueOf("100");     // "100"을 100으로 변환하는 방법2
                                     // 새로운 방법
                                     // 반환값을 참조형이 아닌 기본형으로 해도 문제가 없음
Integer i2 = Integer.valueof("100"); // 원래는 반환 타입이 Integer
```

## String 클래스의 생성자와 메서드
### 생성자
- `String(String s)`
  - 주어진 문자열(S)을 갖는 Stirng인스턴스를 생성
- `String(char[] value)`
  - 주어진 문자열(value)을 갖는 String인스턴스를 생성
- `String(StringBuffer buf)`
  - StringBuffer인스턴스가 갖고 있는 문자열과 같은 내용의 String인스턴스를 생성

### 메서드
- `char charAt(int index)`
  - 지정된 위치에 있는 문자를 알려준다. 이때, 인덱스는 0부터 시작
- `int compareTo(String str)`
  - 문자열과 사전순서로 비교하고, 같으면 0, 등호기준으로 왼쪽의 수가 작으면 음수, 왼쪽의 수가 크면 양수
- `String concat(String str)`
  - 문자열을 뒤에 덧붙인다. 즉, 문자열 결합에 사용
- `boolean contains(CharSequence s)`
  - 지정된 문자열이 포함되었는지 확인
- `boolean endsWith(String suffix)`
  - 지정된 문자열로 끝나는지 검사
- `boolean equals(Object obj)`
  - 매개변수로 받은 문자열과 Stirng인스턴스의 문자열을 비교한 후 obj가 String인스턴스가 아니거나 문자열이 다르면 false를 반환
- `boolean equalsIgnoreCase(String str)`
  - 문자열과 String인스턴스의 문자열과 대소문자 구분없이 비교한다.
- `int indexOf(int ch)`
  - 주어진 문자(ch)가 문자열에 존재하는지 확인하여 위치를 알려준다. 이때 못 찾으면 -1을 반환
- `int indexOf(int ch, int pos)`
  - 주어진 문자(ch)가 문자열에 존재하는지 지정된 위치부터 확인하여 위치를 알려준다. 이때 못 찾으면 -1을 반환
- `int indexOf(String str)`
  - 주어진 문자열이 존재하는지 확인하여 그 위치를 알려준다. 없으면 -1을 반환
- `String intern`
  - 문자열을 상수풀에 등록한다. 이때 상수풀에 같은 내용의 문자열이 있으면 그 문자열의 주소값을 반환한다.
- `int lastIndexOf(int ch)`
  - 지정된 문자 또는 문자코드를 문자열의 오른쪽 끝에서부터 찾아서 위치를 알려준다. 못 찾으면 -1 반환
- `int lastIndexOf(String str)` 
  - 지정된 문자열을 인스턴스의 문자열 끝에서부터 찾아서 위치를 알려준다. 못 찾으면 -1 반환
- `int length()`
  - 문자열의 길이를 알려주다.
- `String[] split(String regex, int limit)` 
  - 문자열을 지정된 분리자(regx)로 나누어 문자열배열에 담아 반환한다. 단, 문자열 전체를 지정된 수로 자른다.
- `boolean startsWith(String prefix)`
  - 주어진 문자열로 시작하는 검사한다.
- `String substrint(int begin), String substrint(int begin, int end)`
  - 주어진 시작위치부터 끝 위치 범위에 포함된 문자열을 얻는다. (begin<=x < end)
- `String toLowerCase()`
  - String인스턴스에 저장되어있는 모든 문자열을 소문자로 변환하여 반환한다.
- `String toString()`
  - String인스턴스에 저장되어있는 문자열을 반환한다.
- `String toUpperCase()`
  - String인스턴스에 저장되어있는 모든 문자열을 대문자로 변환하여 반환한다.
- `String trim`
  - 문자열의 왼쪽 끝과 오른쪽 끝에 있는 공백을 없앤 결과를 반환한다.
- `static String valuof(모든 매개변수),static String valuof(Object o)`
  - 지정된 값을 문자열로 변환하여 반환한다. 이때 참조변수의 경우, toString()을 호출한 결과를 반환한다.

## join() & StringJoiner
- join()과 java.util.StringJoiner은 JDK1.8부터 추가되었다.
## join()
- join()은 여러 문자열 사이에 구분자를 넣어서 결합한다.
```java
String animals = "dog, cat, bear";
String[] arr   = animals.split(",");  // 문자열을 ','를 구분자로 나눠배열에 저장
String str   = String.join("-", arr); // 배열의 문자열로 '-'로 구분해서 결합
System.out.println(str);              // dog-cat-bear
```

## StringJoiner
- 이 클래스를 사용해서 문자열 결합가능
```java
StringJoiner sj = new StringJoiner(",", "[","]");
String[] strArr = { "aaa", "bbb", "ccc" };

for (String s : strArr)
    sj.add(s.toUpperCase());

System.out.println(sj.toString()); // [AAA,BBB,CCC]
```

## 기본형 값을 String으로 변환
```java
int i = 100;

// 첫 번째 방법
String str1 = i + "";           // 코드가 간결하다.

// 두 번째 방법
String str2 = String.valuOf(i); // 연산속도가 빠르다.
```

## String을 기본형 값을 변환
```java
// 첫 번째 방법 - old한 방법
int i = Integer.parseInt("100");

// 두 번째 방법 - 최신 방법(메서드의 이름을 통일하기 위해, 오토방식에 의해 Integer가 int로 자동 변환)
int i2 = Integer.valuOf("100");
```


  
  

# reference
자바의 정석 - 남궁성
