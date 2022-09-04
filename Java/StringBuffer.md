# StringBuffer클래스&StringBuilder클래스
## StringBuffer클래스
- 내부적으로 문자열 배열을 가지고 있다.

- StringBuffer클래스는 String클래스와 다르게 내부적으로 문자열 편집을 위한 버퍼(Buffer)을 가지고 있기 때문에 변경이 가능하다.
- 편집 시 문자열의 길이를 고려해서 버퍼의 길이를 충분히 길게 잡아주는 것이 좋다.(고려해주지 않으면 작업 시 추가로 버퍼의 길이를 늘려주는 작업을 해야 하기 때문에 작업효율이 떨어짐)
- 버퍼의 크기를 지정하지 않는 버퍼의 기본값은 16이다.
- StringBuffer클래스는 equals메서드를 오버라이딩하지 않는다.(==와 같은 결과가 출력)
- toString()은 오버라이딩되어 있어서, StringBuffer인스턴스에 toString()을 호출한 후에, 담고 있는 문자열을 String으로 반환한다.
```java
// 적절한 크기 지정하는 방법
public StringBuffer (int length) {  // int lenght 매개변수를 통해 길이를 지정
  value = new char[length];
  shared = false;
}

// 길이를 지정하지 않으면 버퍼의 기본값이 16으로 반환
public StringBuffer () {
  this(16);
}

// 지정한 문자열의 길이보다 16이 더 크게 버퍼를 생성한다.
public StringBuffer (String str) {
  this(Str.length + 16);
}
```
### StringBuffer의 변경
- 기존에 String클래스의 배열을 추가하는 방법
  1. 새로운 배열을 생성시킨다.
  2. 기존의 값의 내용을 복사시킨다.
  3. 새롭게 생성된 배열에 대해 참조시킨다.

- StirngBuffer클래스의 배열을 추가하는 방법
```java
String sb = new StringBuffer("abc");
//sb.append("123");
//sb.append("zz");
sb.append("123").append("zz");  // 한줄로 표현 가능, 
``` 

## StringBuffer클래스의 생성자와 메서드
### 생성자
- `StringBuffer()`<br>
  :16문자를 담을 수 있는 버퍼를 가진 StringBuffer 인스턴스를 생성
- `StringBuffer(int length)`<br>
  :지정된 개수의 문자를 담을 수 있는 버퍼를 가진 StirngBuffer 인스턴스를 생성
- `StringBuffer(String str)`<br>
  :지정된 문자열 값(str)을 갖는 StringBuffer 인스턴스를 생성

### 메서드
- `StringBuffer append(모든 기본형 타입의 매개변수 & 문자열 & 참조변수)`<br>
  :매개변수로 입력된 값을 문자열로 변환하여 StringBuffer인스턴스가 저장하고 있는 문자열의 뒤에 덧붙임
- `int capactiy()`<br>
  :StringBuffer인스턴스의 버퍼크기를 알려준다.
- `char charAt(int index)`<br>
  :지정된 위치에 있는 문자를 반환한다.
- `StringBuffer delet(int start, int end)`<br>
  :시작위치부터 끝 위치 사이에 있는 문자를 제거, 이때 끝 위치의 문자를 제외, 빈자리는 땡겨짐
- `StringBuffer deletCharAt(int index)`<br>
  :지정된 위치의 문자를 제거한다. 이때 빈자리는 땡겨짐
- `StringBuffer insert(지정된 위치, 모든 기본형 타입의 매개변수 & 문자열 & 참조변수)`<br>
  :두 번째 매개변수로 받은 값을 문자열로 변환하여 지정된 위치에 추가, 이때 지정된 위치는 0부터 시작
- `int length`<br>
  :StringBuffer 인스턴스에 저장되어 있는 문자열의 길이를 반환
- `StringBuffer replace(int start, int end, String str)`<br>
  :지정된 범위의 문자들을 주어진 문자열로 바꿈. 이때, start<= x < end
- `StringBuffer reverse`<br>
  :StringBuffer 인스턴스에 저장되어 있는 문자열의 순서를 거꾸로 나열
- `void setCharAt(int index, char ch)`<br>
  :지정된 위치의 문자를 주어진 문자(ch)로 바꿈
- `void setLength(int newLength)`<br>
  :지정된 길이로 문자열의 길이를 변경. 이때, 길이를 늘리는 경우에 나머진 빈 공간은 널문자 '\u0000'로 채운다.
- `String toString()`<br>
  :StringBuffer인스턴스의 문자열을 String으로 반환
- `String substring(int start or int start, int end)`<br>
  :지정된 범위 내의 문자열을 String으로 뽑아서 반환.이때 시작위치만 지정하면 문자열 끝까지 뽑아서 반환함. start<= x < end


## StringBuilder
- StringBuffer와 매우 유사하다.

- StringBuilder는 StringBuffer와 다르게 동기화 기능만 뺀 기능이다.
- 동기화란 멀티 쓰레드에서 데이터를 공유하는데, 이렇게 되면 데이터가 꼬이는 현상이 발생하게 된다. 이때 동기화는 데이터가 꼬이는 것을 막아준다.
- 싱글쓰레드의 경우 동기화는 성능을 저하시키는 역할을 하게 된다.
- 그래서 동기화 기능만 뺀 새로운 StringBuilder가 추가 되었다. 
- StringBuffer의 생성자만 바꾸면 StringBuilder로 사용할 수 있다.

# reference
자바의 정석 - 남궁성
