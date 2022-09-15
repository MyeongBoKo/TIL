# Iterator & ListIterator & Enumeration
## 1. Iterator & ListIterator & Enumeration란
- 모두 컬렉션에 저장된 요소를 접근하는데 사용되는 인터페이스.
- Enumeration은 Iterator의 구버전
- ListIterator은 Iterator의 기능을 향상 시킨 것

## 2. Iterator란
- 컬렉션에 저장된 요소들을 읽어오는 방법을 표준화 한 것 
- 컬렉션에 저장된 각 요소에 접근하는 기능을 가진 Iterator 인터페이스 정의
- 컬렉션에는 Iterator(Iterator를 구현한 클래스의 인스턴스)를 반환해주는 iterator()를 정의하고 있다. 
```java
Public interface Iterator {
    boolean hasNext();
    Object next();
    void remove();
}

public interface Collection {
    ...
    public Iterator iterator();
    ...
}
```
## 3. Iterator인터페이스의 메서드
메서드|설명
--|--
boolean hasNext()|읽어올 요소가 남아있는지 확인
Object next()|다음 요소를 읽음
void remove()|next()로 읽어온 요소를 삭제

```java
// ArrayList에 저장된 요소들을 출력

Collection c = new ArrayList();     // 다른 컬렉션으로 변경시 이 부분을 고친다.       
Iterator it = c.iterator();         // iterator의 객체를 반환

while(it.hasNext()) {               // 읽어올 요소 확인
    System.out.println(it.next())   // 다음 요소 읽기
}
```

### Ex)11-13
```java
import java.util.*;

class IteratorEx1 {
    public static void main(String[] args) {
        ArrayList list = new ArrayList();   // ArrayList는 Collection클래스의 자손이기 때문에 이렇게 작성해도 상관없다. 하지만 Collcetion클래스로 작성하는 것이 코드를 유지 보수하는데 적합하기 때문에 후자를 권장
        list.add("1");
        list.add("2");
        list.add("3");
        list.add("4");
        list.add("5");

        Iterator it = list.iterator();  // iterator를 통해서 다 읽으면 끝나기 때문에 다시 값을 얻기 위해서는 iterator 객체를 얻어야 한다.

        while (it.hasNext()) {      // 읽어올 요소 확인
            Object obj = it.next(); // 다음 요소 읽은 것을 객체에 저장
            System.out.println(obj);// 출력
        }
    }
}
```

## 4. Map에서의 iterator
- Map에서는 iterator을 직접 호출할 수 없다.

- keySet() 또는 entrySet()과 같은 메서들을 통해 키와 값을 따로 Set의 형태로 얻은 다음에 다시 iterator()를 호출해야 Iterator을 얻을 수 있다.
```java
Map map = new HashMap();
Iterator it = map.entrySet.iterator();
//Set eSet = map.entrySet();
//Iterator it = eSet.iterator;
```
### 실행순서
#### Iterator it = map.entrySet.iterator();
1. map.entry()의 실행결과가 Set
    - Iterator it = map.entrySet.iterator(); -><br>
  Iterator it = Set인스턴스.iterator();

2. map.entrySet()를 통해 얻은 Set인스턴스의 iterator()를 호출해서 Iterator를 얻는다.
    - Iterator it = Set인스턴스.iterator(); -><br>
  Iterator it = Iterator인스턴스;
3. 마지막으로 Iterator인스턴스의 참조가 it에 저장된다.

## 5. ListIterator & Enumeration
### ListIterator
- Iterator에 양방향 조회기능추가(List를 구현한 경우만 사용가능)

### ListIterator의 메서드
메서드|설명
--|--
void add(Object o)|컬렉션에 새로운 객체를 추가
boolean hasNext()|읽어 올 다음 요소가 남아있는지 확인
boolean hasPrevious()|읽어 올 이전 요소가 남아있는지 확인
Object next()|다음 요소를 읽음
Object previous()|이전 요소를 읽음
int nextIndex()|다음 요소의 index를 반환
int previousIndex()|이전 요소의 index를 반환
void remove()|next() 또는 previous()로 읽어 온 요소를 삭제
void set(Object o)|next() 또는 previous()로 읽어 온 요소를 지정된 객체로 저장

### Enumeration
- Iterator의 구버전

### Enumeration인터페이스 메서드
메서드|설명
--|--
boolean hasMoreElements()|읽어 올 요소가 남아있는지 확인
Object nextElement()|다음 요소를 읽음

# reference
자바의 정석 - 남궁성
