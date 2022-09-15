# LinkedList
## 1. 배열의 장단점
1. 장점
   - 구조가 간단하며 사용하기 쉽다.
   - 데이터를 읽어오는데 걸리는 시간(접근시간)이 빠르다.
   - index가 n인 데이터의 주소 = 배열의 주소 + n * 데이터 타입의 크기
2. 단점
   1. 크기를 변경할 수 없다.
       - 크기를 변경할 수 없기 때문에 새로운 배열을 생성해서 데이터를 복사해야 한다.
       - 실행속도를 향상시키기 위해 충분히 큰 크기의 배열을 생성해야 하기 때문에 메모리가 낭비된다. 
   2. 비순차적인 데이터의 추가 또는 삭제에 시간이 많이 걸린다.
       - 차례대로 데이터를 추가하고 마지막에서부터 데이터를 삭제하는 것이 빠르다.
       - 배열의 중간에 데이터를 추가하려면, 빈자리를 만들기 위해 다른 데이터들을 복사해서 이동해야 한다.

## 2. 링크드리스트(LinkedList)
- 위의 배열을 단점을 보완하기 위해 링키드리스트 자료구조가 고안되었다.
- 불연속적으로 존재하는 데이터를 서로 연결한 형태로 구성되었다.
- 링키드 리스트의 각 요소(node)들은 자신과 연결된 다음 요소에 대한 참조(주소값)와 데이터로 구성
```java
class Node {
    Node next;  // 다음 요소의 주소 저장
    Object obj; // 데이터를 저장
}
```

### 링크드리스트에서 데이터 삭제
- 데이터 삭제는 간단하다
- 단 하나의 참조만 변경하면 삭제가 이루어진다.

### 링크드리스트에서 데이터 추가
1. 새로운 요소를 생성
2. 추가하고자 하는 위치의 이전 요소의 참조를 새로운 요소에 대한 참조로 변경
3. 새로운 요소가 그 다음 요소를 참조하도록 변경
    - 한 번의 Node 객체생성과 두번의 참조변경만으로 가능하기 때문에 처리속도가 매우 빠르다.

### 링크드리스트 단점
- 데이터 접근성이 나쁨(한번에 이동 불가)
- 이동방향이 단방향이기 때문에 이전 요소에 대해 접근이 어렵다. 

## 3. 이중 연결 리스트(더블 링크드 리스트)
- 이중 연결리스트, 접근성 향상
- 단순히 링크드 리스트에 참조변수 하나 더 추가하여 다음 요소에 대한 참조뿐만 아니라 이전 요소에 대한 참조가 가능할 뿐 그 외는 링키드 리스트와 같다.
- 각 요소에 대한 접근이 쉽기 때문에 자바에서는 이중 연결 리스트로 구현되었다.
```java
class Node{
    Node next;      // 다음 요소의 주소를 저장
    Node previous;  // 이전 요소의 주소를 저장
    Object obj;     // 데이터를 저장
}
```

## 4. 더블 써큘러 링크드 리스트
- 이중 원형 연결리스트
- 더블 링크드 리스트의 첫 번째 요소와 마지막 요소를 서로 연결
- 더블 링크드 리스트의 접근성을 더욱 향상 시킨 구조이다.

## 5. LinkedList메서드
생성자|설명
--|--
LinkedList()|LinkedList 객체를 **생성**
LinkedList(Colleciton s)| 주어지 컬렉션을 포함하는 LinkedList객체를 **생성**

*boolean이 붙은 메서드는 성공하면 true반환, 실패하면 false반환*

메서드(추가)|설명
--|--
boolean add(Object o)|지정된 객체를 LinkedList의 끝에 **추가**<br>성공하면 true, 실패하면 false
boolean addAll(Collection c)|주어진 컬렉션에 포함된 모든 요소를 LinkedList의 끝에 **추가**<br>성공하면 true, 실패하면 false
void add(int index, Object element)|지정된 위치에 객체를 **추가**
boolean addAll(int index, Collection c)|지정된 위치에 컬렉션에 포함된 모든 요소를 **추가**<br>성공하면 true, 실패하면 false

메서드(삭제)|설명
--|--
void clear()|LinkedList의 모든 요소들을 **삭제**
object remove(int index)|지정된 위치의 객체를 LinkedList에서 **삭제**
boolean remove(Object o)|지정된 객체를 LinkedList에서 **삭제**
boolean removeAll(Collection c)|지정된 컬렉션의 요소와 일치하는 요소를 **모두 삭제**

메서드(검색)|설명
--|--
boolean contains(Object o)|지정된 객체가 LinkedList에 **포함되었는지 *알려줌**
boolean containsAll(Collection c)|지정된 컬렉션의 모든 요소가 **포함되었는지 알려줌**
Object get(int index)|지정된 위치의 **객체를 반환**
int indexOf(Object o)|지정된 객체가 **저장된 위치를 반환**<br> ->
int lastindexOf(Object o)|지정된 객체가 **저장된 위치를 반환**<br> <-
boolean isEmpty()|LinkedList가 **비었는지 알려줌**
boolean retainAll(Collection c)|지정된 컬렉션의 모든 요소가 포함되어 있는지 **확인**
Iterator iterator()|**iterator 반환**
ListIterator listiterator()|**ListIterato 반환**
ListIterator listiterator(int index)|지정된 위치에서부터 시작하는 **ListIterato 반환**
int size()|LinkedList에 **저장된 객체의 수를 반환**

메서드|설명
--|--
Object set(int index, Object element)|지정된 위치의 객체를 주어진 객체로 바꿈
List subList(int fromIndex, toIndex)|LinkedList의 일부를 List로 반환
Object[] toArray()|LinkedList에 저장된 객체를 배열로 반환
object[] toArray(Object[] a)|LinkedList에 저장된 객체를 주어진 배열에 저장하여 반환

#### Queue인터페이스와 Deque인터페이스를 구현하면서 추가된 메서드
메서드(Queue인터페이스)|설명
--|--
Object element()|LinkedList의 첫 번째 요소를 반환
boolean offer(Object o)|지정된 객체를 LinkedList의 끝에 추가
Object peek()|LinkedList 첫 번째 요소를 반환
Object poll()|LinkedList의 첫 번째 요소를 반환.<br>LinkedList에서는 제거
Object remove()|LinkedList의 첫 번째 요소를 제거

메서드(Deque인터페이스)|설명
--|--
void addFirst(Object o)|LinkedList의 맨 앞에 객체를 추가
void addLast(Object o)|LinkedList의 맨 끝에 객체를 추가
Iterator descendingIterator()|역순으로 조회하기 위한 DescendingIterator를 반환
Object getFirst()|LinkedList의 첫번째 요소를 반환
Object getLast()|LinkedList의 마지막 요소를 반환
boolean offerFirst(Object o)|LinkedList의 맨 앞에 객체를 추가
boolean offerLast(Object o)|LinkedList의 맨 끝에 객체를 추가
Object peekFirst()|LinkedList의 첫번째 요소를 반환
Object peekLast()|LinkedList의 마지막 요소를 반환
Object pollFirst()|LinkedList의 첫번째 요소를 반환하면서 제거
Object pollLast()|LinkedList의 마지막 요소를 반환하면서 제거
Object pop()|removeFirst()와 동일
void push(Object o)|addFirst()와 동일
Object removeFirst()|LinkedList의 첫번째 요소를 제거
Object removeLast()|LinkedList의 마지막 요소를 제거
boolean removeFirstOccurrence(Object o)|LinkedList에서 첫번째로 일치하는 객체를 제거
boolean removeLastOccurrence(Object o)|LinkedList에서 마지막으로 일치하는 객체를 제거

# reference
자바의 정석 - 남궁성
