# 컬렉션 프레임웍(collections framework)
## 1. 컬렉션 프레임웍이란
- 컬렉션(collection):<br>
  1.여러 객체(데이터)를 모아 놓은 것을 의미
- 프레임웍(framework):<br>
  1.표준화, 정형화된 체계적인 프로그래밍 방식(프로그래밍 방식 + 라이브러리(기능))   
  2.자유도는 떨어지지만, 생산성과 유지보수에는 장점이 있다.
- 컬렉션 프레임웍(collection framework):<br>
  1.컬렉션(다수의 객체)을 다루기 위한 표준화된 프로그래밍 방식   
  2.컬렉션을 쉽고 편리하게 다룰 수 있는 다양한 클래스를 제공   
  3.이때 다수의 객체를 다룬다는 것은 객체를 저장, 삭제, 검색, 정렬을 의미한다.   
  4.java.util패키지에 포함. JDK1.2부터 제공한다.    
- 컬렉션 클래스(collection class):<br>
  1.다수의 데이터를 저장할 수 있는 클래스(예, Vector, ArrayList, Hashset)      

## 2. 컬렉션 프레임웍의 핵심 인터페이스
- 핵심 3가지 타입 **'List', 'Set', 'Map'**
- List와 set의 공통된 부분을 다시 뽑아서 새로운 인터페이스인 **Collection**을 정의
- **List**:<br>
  저장순서O, 중복O
- **Set**:<br>
  저장순서X, 중복X
- **Map**:<br>
  저장순서X, 중복O - value(값), 중복X - key(키) 

인터페이스|특징
--|--
List|순서가 있는 데이터의 집합, 데이터의 중복 허용한다.<br> ex) 대기자 명단<br>구현클래스: ArrayList, LinkedList, Stack, Vector 등
Set|순서를 유지하지 않는 데이터의 집합, 데이터의 중복 허용하지 않는다.<br> ex) 양의 정수 집합, 소수의 집합 <br> 구현클래스: HashSet, TreeSet 
Map|키(key)와 값(value)의 쌍으로 이루어진 데이터의 집합. 순서는 유지되지 않으며, 키는 중복을 허용하지 않고, 값은 중복을 허용한다. <br> ex) 우편번호, 지역번호<br> 구현클래스: HashMap, TreeMap, Hashtable, Properties 등

## 3. Collection 인터페이스
메서드|설명
:--|:--
boolean add(Object o)<br>boolean addAll(Collection c) | 지정된 객체(o) 또는 Collection (c)의 객체들을 Collection에 **추가**
void clear()| Collection의 모든 객체를 **삭제**
boolean contains(Object o)<br> boolean containsAll(Collection c)| 지정된 객체(o) 또는 Collection의 객체들이 Collection에 포함되어 있는지 **확인** 
boolean equals(Object o)| 동일한 Collection인지 **비교**
int hashCode()| Collection의 hash code를 **반환**
boolean isEmpty()| Collection이 비어있는지 **확인**
lterator iterator()|Collection의 lterator를 얻어서 **반환**
boolean remove(Object o)|지정된 객체를 **삭제**
boolean removeAll(Collection c)|지정된 Collection에 포함된 객체를 **삭제**
boolean retainAll(Collection c)|지정된 Collection에 포함된 객체만 남기고,다른 Collection에서 **삭제**<br> 이 작업으로 인해 Collection에 **변화가 있다면 true 그렇지 않으면 False 반환**
int size()| Collection에 저장된 객체의 개수를 **반환**
Object[] toArray()|Collection에 저장된 객체를 객체배열(Object[])로 **반환**
Object[] toArray(Object[] a|지정된 배열에 Collection의 객체를 저장해서 **반환**

## 4. List 인터페이스
메서드|설명
:--|:--
void add(int index, Object element)<br>boolean addAll(int index, Collection C)|지정된 위치에 객체 또는 컬렉션에 포함된 객체를 **추가**
Object get(int index)|지정된 위치에 있는 객체를 **반환**
int indexOf(Object o)|지정된 객체의 위치를 **반환**<br>왼 -> 오
int lastIndexOf(Object o)|지정된 객체의 위치를 **반환**<br>오 -> 왼
Listlterator listlterator()<br>Listlterator listlterator(int index)|List의 객체에 접근할 수 있는 Litlterator를 **반환**
Object remove(int index)|지정된 위치에 있는 객체를 **삭제**하고 삭제된 객체를 **반환**
Object set(int index, Object element)|지정된 위치에 객체를 **저장**
void sort(Compareator c)|지정된 비교자로 List를 **정렬**
List subList(int fromIndex, int toIndex)|지정된 범위에 있는 객체를 **반환**<br>일부를 뽑아온다.

## 5. Set 인터페이스
- Set 인터페이스는 List 인터페이스와 유사하다.
- 집합과 관련된 메서드(Collection에 변화가 있으면 true, 아니면 false를 반환)

메서드|설명
--|--
boolean addAll(Collection c)|지정된 Colection(c)의 객체들을 Collection에 **추가(합집합)**
boolean containsAll(Collection c)|지정된 Colection(c)의 객체들을 Collection에 포함되어 있는지 **확인 (부분집합)**
boolean removeAll(Collection c)|지정된 Colection(c)에 포함된 객체들을 **삭제(차집합)**
boolean retainAll(Collection c)|지정된 Colection(c)에 포함된 객체만을 남기고, 나머지는 Collection에서 **삭제 (교집합)**

## 6. Map 인터페이스
메서드|설명
--|--
void clear()|Map의 모든 객체를 **삭제**
boolean containsKey(Object key)|지정된 key객체와 일치하는 Map의 key객체가 있는지 **확인**
boolean vontainsValue(Object value)|지정된 value객체와 일치하는 Map의 value객체가 있는지 **확인**
Set entrySet()|Map에 저장되어 있는 key-value쌍을 Map.value쌍을 Map.Entry타입의 객체로 저장한 Set **반환**
boolean equals(Object o)|동일한 Map인지 **비교**
Object get(Object key)|지정한 key객체에 대응하는 value객체를 찾아서 **반환**
int hashCode()|해시코드를 **반환**
boolean isEmpty|Map이 비어있는지 **확인**
Set keySet()|Map에 저장된 모든 key객체를 **반환**
Object put(Object key, Object value)|Map에 value객체를 key객체에 연결하여 **저장**
void putAll(Map t)|지정된 Map의 모든 key-value쌍을 **추가**
Object remove(Object key)|지정한 key객체와 일치하는 key-value객체를 **삭제**
int size()|Map에 저장된 key-value쌍의 개수를 **반환**
Collection values()|Map에 저장된 모든 value객체를 **반환**

## 7. Map.Entry인터페이스
- Map인터페이스의 내부 인터페이스
- 내부 클래스와 같이 인터페이스도 인터페이스 안에 인터페이스를 정의하는 내부 인터페이스 정의 가능   

메서드|설명
--|--
boolean equals(Object o)|동일한 Entry인지 **비교**
Object getKey()|Entry의 key객체를 **반환**
Object getValue()|Entry의 value객체를 **반환**
int hashCode()|Entry의 해시코드를 **반환**
Object setValue(Object value)|Entry의 value객체를 지정된 객체로 **변경**

# reference
자바의 정석 - 남궁성


