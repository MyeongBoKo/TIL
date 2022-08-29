# 내부 클래스(inner class)
## 내부 클래스란
클래스 내에 선언된 클래스이다.
```java
// 일반 클래스
class A {
    ...
}
class B {
    ...
}
```
```java
// 내부 클래스
class A {           // A는 B의 외부 클래스
    ...
     class B {   // B는 A의 내부 클래스
        ...
     }
}
```

## 내부 클래스를 사용했을 때 장점
1. 내부 클래스에서 외부 클래스의 맴버들을 쉽게 접근할 수 있다.
   - 일반 클래스의 경우 다른 클래스에서 접근 허용하게 하려면 객체를 생성해야 한다.
   - 내부 클래스의 경우 객체 생성없이 맴버의 접근이 가능하다.
  

2. 코드의 복잡성을 줄일 수 있다. (캡슐화)
   
## 내부 클래스의 종류와 특징
```java
class Outer {
    int iv = 0;         // 1. iv
    static int cv = 0;  // 2. cv

    void myMethod(); {
        int lv = 0;     // 3. lv
    }
}


class Outer {
    class InstanceInner {}       // 1. 인스턴스 내부 클래스
    static class StaticInner {}  // 2. 스태틱 내부 클래스

    void myMethod() {
        class LocalInner {}      // 3. 지역 내부 클래스
    }
}
```

## 내부 클래스의 제어자와 접근성
- 내부 클래스는 접근 제어자 4개 가능하다.(default, public, abstract, final)

- 멤버변수들처럼 privated, protected과 접근제어자도 사용이 가능
- static 내부 클래스에서는 외부 클래스의 인스턴스 멤버에 접근할 수 없다.
- 내부 클래스를 작성하는데 static 멤버가 필요하면, 내부  클래스로 static 클래스가 되야 한다. 즉, static 클래스만 static멤버를 정의할 수 있다.
- 인스턴스멤버 간에는 서로 직접 접근 가능하고, static 멤버 간에는 서로 직접 접근 가능하다.
- static 멤버는 인스턴스 멤버에 직접 접근할 수 없다.
  - 접근하려면 먼저, 인스턴스클래스는 외부 클래스를 먼저 생성해야만 한다.
- 인스턴스메서드에서는 인스턴스 멤버와 static 멤버 모두 접근가능하다.
- 메서드 내에 지역적으로 선언된 내부 클래스는 외부에서 접근 불가 
```java
public class Inner_class_2 {
	class InstanceInner {}		// 인스턴스 멤버
	static class StaticInner {}
	
	InstanceInner iv = new InstanceInner();			// 인스턴스멤버끼리 직접 접근 가능
	static StaticInner cv = new StaticInner();		// static 멤버끼리는 직접 접근 가능
	
	static void staticMethod() {					// static 멤버는 인스턴스 멤버에 직접 접근 불가
//		InstanceInner obj1 = new InstanceInner();
		StaticInner obj2 = new StaticInner();
		
		Inner_class_2 Outer = new Inner_class_2();	// 인스턴스클래스는 외부 클래스를 먼저 생성해야 생성가능
		InstanceInner obj1 = Outer.new InstanceInner();
	}
	
	void instanceMethod() {							// 인스턴스메서드에서는 인스턴스 멤버와 static 멤버 모두 접근 가능		
		InstanceInner obj1 = new InstanceInner();
		StaticInner obj2 = new StaticInner();
//		LocalInner lv = new LocalInner();			// 지역 내부 클래스는 외부에서 접근할 수 없다.
	}
	
	void myMethod() {
		class LocalInner {}
		LocalInner lv = new LocalInner();
	}
	
	public static void main(String[] args) {
		// TODO Auto-generated method stub

	}

}
```
- 외부 클래스의 private멤버도 접근가능하다.
- 지역 내부 클래스를 감싸고 있는 메서드의 상수만 사용가능.
```java
public class Inner_class_3 {
	private int outerIv = 0;
	private static int outerCv = 0;
	
	class InstanceInner {
		int iiv = outerIv;		// 1. 외부 클래스의 private멤버도 접근가능하다.
		int iiv2 = outerCv;
	}
	
	static class StaticInner {
//	스태틱 클래스는 외부 클래스의 인스턴스멤버에 접근할 수 없다.		
//		int siv = outerIv;
		static int scv = outerCv;
	}
	
	void myMethod() {
//	final을 사용해야 하는 이유는 만약 final을 사용하지 않으면 지역변수이기 때문에 메소드가 종료와 함께 소멸한다. 이때 내부 클래스의 객체는 지역변수보다 더 오래 존재할 수 있기 때문에 final을 붙여야 한다.		
// 	상수는 따로 저장해서 사용된다.
		final int lv = 0;	// 값이 바뀌지 않는 변수는 상수로 취급한다.
		final int Lv = 0;	// JDK1.8부터 final 생략 가능
		
		class LocalInner {	// 2. 지역 내부 클래스를 감싸고 있는 메서드의 상수만 사용가능.
			int liv = outerIv;
			int liv2 = outerCv;
//	외부 클래스의 지역변수 final이 붙은 변수(상수)만 접근가능하다.
//			int liv3 = lv;  // 에러!!!(JDK1.8부터 에러 아님)
			int liv4 = Lv;	// OK
		}
			
	}
	

}
```
<내부 클래스를 생성하고 내부 클래스의 멤버에 접근하는 방법>
```java
Outer oc = new Outer(); 
Outer.InstanceInner ii = oc.new InstanceInner();
```
1. 외부 클래스의 인스턴스를 생성
2. 내부 클래스의 인스턴스를 생성

```java
Outer.StaticInner.cv;
Outer.StaticInner si = new Outer.StaticInner();		// 이때 
```
- 객체를 생성하지 않고 바로 사용가능하다. (static내부 클래스)
- static 내부 인스턴스 생성할 때 외부클래스의 이름을 붙여야 한다. 이때 static 내부의 인스턴스는 외부 클래스를 먼저 생성하지 않아도 된다.
  
# 익명 클래스(anonymous class)
## 익명 클래스란
- 이름이 없는 클래스
- 한번만 사용되는 클래스

### 작성법
```java
new 조상클래스이름 () {
    // ...
}

new 구현인터페이스이름() {
    //...
}
```
- {} 안에는 클래스 내용이 들어간다.
- 이름이 없기 때문에 조상클래스 이름 또는 인터페이스의 이름을 사용한다.

# reference
자바의 정석 - 남궁성
