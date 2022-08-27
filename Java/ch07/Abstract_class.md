# 추상클래스(abstract class)
## 추상클래스란
- 미완성 클래스 즉 미완성 설계도

- 이때 클래스가 미완성이란 의미는 맴버의 개수에 관계있는 것이 아닌 단지 클래스가 미완성 메서드를 포함하는 것을 의미
- 선언문 맨 앞에 'abstract'을 작성한다.
  
## 추상메서드(abstract method)
- 선언부만 작성하고 구현부는 작성하지 않고 남겨 둔 것을 말한다.

- 몸통이 없는 메서드를 의미한다.
- 자손클래스는 조상클래스로부터 상속받은 추상메서드를 모두 구현해야 한다.
- 추상메서드 역시 'abstract'를 앞에 붙여 주고, 구현부가 없기 때문에 {}대신 ;으로 끝을 알림.

```java
abstract class Player { // 추상 클래스
    abstract void play(int pos);    // 추상 메서드
    abstract void stop();           // 추상 메서드
}

class AudioPlayer extends Player {
    void play(int pos) { /* 내용 생략 */ }  // 추상 메서드 구현
    void strop() {/* 내용 생략 */}          // 추상 메서드 구현
}

// 조상으로부터 상속받은 메서드의 개수는 2개 이기 때문에 아래의 class의 경우 미완성 클래스이다. 그래서 abstract를 붙여서 추상 클래스화해야 한다.
abstract class AudioPlayer extends Player {
    void play(int pos) {/* 내용 생략 */}
}

// 아니면 아래와 같이 표현해야 한다. 자손 클래스는 상속받은 추상 메서드를 구현해야 한다. 만약 구현하지 못하는 경우 자손 클래스 역시 추상 클래스로 지정해줘야 한다.
abstract class AudioPlayer extends Player {
    void play(int pos) {/* 내용 생략 */}
    abstract void stop(); 
}

```
## 추상클래스의 작성
- 객체지향에서 추상은 단순한 추상을 넘는 의미를 가지고 있다.
- 추상화는 구체화와 상반되는 단어로써 불명확하다는 의미를 지니고 있다.
- 불명확하고 구체적이지 않는 추상화를 사용하는 이유는 무엇인가? 
  - 추상화된 코드는 구체화된 코드보다 유연하고, 변경에 유리하다.
  - 중복된 코드를 제거하기 용이하다.
  - 추상클래스를 단계별로 만들면, 코드를 유연하게 작성하는 것에 용이하다.

# reference
자바의 정석 - 남궁성
