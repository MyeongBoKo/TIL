# Stack & Queue
## Stack
- 스택은 마지막에 저장한 데이터를 가장 먼저 꺼내게 되는 LIFO(Last In First out)구조

- 양 옆과 바닥이 막혀 있어서 한 방향으로만 뺄 수 있는 구조
- 저장을 push, 추출을 pop
- 데이터를 순차적으로 추가하고 삭제하는 스택은 ArrayList와 같은 배열기반의 컬렉션 클래스가 적합
- 스태은 Stack클래스로 구현

## Stack메서드
메서드|설명
--|--
boolean empty()|Stack이 비어있는지 알려준다.
Object peek()|Stack의 맨 위에 있는 저장된 객체를 반환. pop()과 달리 Stack에서 객체를 꺼내지 않는다.<br>Stack이 비어있을때 예외 발생
Object pop()|Stack의 맨 위에 저장된 객체를 꺼낸다. <br>Stack이 비어있을때 예외 발생
Object push(Object item)|Stack에 객체(item)를 저장
int search(Object o)|Stack에서 주어진 객체를 찾아서 그 위치를 반환. 못찾으면 -1을 반환<br>(배열과 달리 위치는 0이 아닌 1부터 시작)

## Queue
- 큐는 처음에 저장한 데이터를 가장 먼저 꺼내게 되는 FIFO(First In First Out)구조

- 양 옆만 막혀 있고 위아래는 뚫려 있어서 한 방향으로는 넣고 한 방향으로는 뺄 수 있다.
- 큐는 데이터를 꺼낼 때 항상 첫 번째 저장된 데이터를 삭제하기 때문에 ArrayList와 같은 배열기반의 컬렉션 클래스를 사용하면 데이터를 꺼낼 때마다 빈 공간을 채우기 위해 데이터의 복사해야 하기 때문에 비효율적이다.
- 큐는 ArrayList보다 데이터의 추가/삭제가 쉬운 LinkedList로 구현하는 것이 적합
- 큐는 Queue인터페이스로 구현(객체 생성 불가)

## Queue 메서드
메서드|설명
--|--
boolean add(Object o)|지정된 객체를 Queue에 추가.<br>저장공간이 부족하면 예외발생
Object remove()|Queue에 객체를 꺼내 반환<br>비어있으면 예외발생
Object element()|삭제없이 요소를 읽는다. peek와 달리 Queue가 비어있을때 예외발생
boolean offer(Object o)|Queue에 객체를 저장<br>예외발생X
Object poll()|Queue에서 객체를 꺼내서 반환<br>예외발생X
Object peek()|삭제없이 요소를 읽어 온다. <br>Queue가 비어있으면 null을 반환 <br>예외발생X

## Queue의 인터페이스 기능 사용
1. Queue를 직접 구현
2. Queue인터페이스를 구현한 클래스 사용
```java
Queue q = new LinkedList();
q.XXX();
```

# reference
자바의 정석 - 남궁성
