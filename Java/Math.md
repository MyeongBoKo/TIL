# Math클래스
## Mah클래스란
- 수학관련 메서드로 구성
- Math클래스의 메서드는 모두 static

## Math클래스의 메서드
- `static (double, float, int, long) abs(double, float, int, long의 매개변수)` <br>
  :주어진 값의 절대값을 반환한다.
- `static double ceil(double a)`<br>
  :주어진 값을 올림하여 반환한다.
- `static double floor(double a)`<br>
  :주어진 값을 버림하여 반환한다.
- `static (기본형 타입) max(기본형 매개변수, 기본형 매개변수)`<br>
  :주어진 두 값을 비교하여 큰 쪽을 반환한다.
- `static (기본형 타입) min(기본형 매개변수, 기본형 매개변수)`<br>
  :주어진 두 값을 비교하여 작은 쪽을 반환한다.
- `static double random()`<br>
  :0.0 ~ 1.0 범위의 임의의 double값을 반환한다. 이때 1.0은 범위에 포함하지 않는다.
- `static double rint(double a)`<br>
  :짝수 반올림
- `static long round(double a or float a)`<br>
  :반올림

# 래퍼(wrapper) 클래스 
## 래퍼
- 기본형 변수도 객체로 다루어야 할 때 작업을 수행할 수 있게 해주는 클래스를 래퍼 클래스라고 한다.
- 8개의 기본형들을, 이 래퍼 클래스를 이용하면 기본형 값을 객체로 다룰 수 있다.

### 기본형
- boolean - wrap class: Boolean<br>

- char - wrap class: Character<br>
  
- byte - wrap class: Byte<br>

- short - wrap class: short<br>

- int - wrap class: Integer<br>

- long - wrap class: Long<br>

- float - wrap class: Float<br>

- double - wrap class: Double<br>

# reference
자바의 정석 - 남궁성
