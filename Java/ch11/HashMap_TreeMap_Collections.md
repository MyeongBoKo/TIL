# HashMap
## 1. HashMap & Hashtable
- 순서X, 중복(키X, 값O)
- Map인터페이스를 구현, 데이터를 키와 값의 쌍으로 저장
- HashMap(동기화x)은 Hashtable(동기화o)의 신버전
- HashMap 사용을 권장

### HashMap
- Map인터페이스를 구현한 대표적인 컬렉션 클래스

- HashMap의 경우 순서를 유지하려면, LinkedHashMap클래스를 사용하면 된다.
- 해싱(hashing)기법으로 데이터를 저장. 데이터가 많아도 검색이 빠르다.
- Map인터페이스를 구현. 데이터를 키와 값의 쌍으로 저장
- 키와 값을  각각 Object타입으로 저장. (Object, Object)의 형태로 저장하기 때문에 어떠한 객체도 저장할 수 있지만, 키는 주로 String을 대문자 or 소문자로 통일한다.
```java

public class HashMap extends AbstractMap implements Map, Cloneable, 
    Serializable
{
    // 키와 값을 하나의 배열로 저장. 하나의 배열로 다루는 것이 데이터의 무결성적인 측면에서 더 바람직
    transient Entry[] table;
    ...
    static class Entry implements Map.Entry {
        final Object key;
        Object value;
        ...
    }
}
```
### 해싱 - 해시테이블에 저장된 데이터를 가져오는 과정
1. 해시함수를 이용해서 데이터를 해시테이블에 저장하고 검색하는 기법
2. 키로 해시함수를 호출해서 해시코드(배열의 인덱스)를 얻는다.
3. 해시코드(해시함수의 반환값)에 대응하는 링크드리스트를 배열에서 찾는다.
4. 링크드리스트에서 키와 일치하는 데이터를 찾는다.
- 해시함수는 같은 키에 대해 항상 같은 해시코드를 반환해야 한다.
- 서로 다른 키일지라도 같은 값의 해시코드를 반환할 수 있다.

## 2. HashMap의 메서드
생성자|설명
--|--
HashMap()|HashMap객체를 생성
HashMap(int initialCapacity)|지정된 값을 초기용량으로 하는 HashMap객체를 생성
HashMap(int initialCapacity, float loadFactor)|지정된 용량과 load factor의 HashMap객체를 생성
HashMap(Map m)|지정된 Map의 모든 요소를 포함하는 HashMap을 생성

메서드|설명
--|--
void clear()|HashMap에 저장된 모든 객체를 제거
Object clone()|현재 HashMap을 복제해서 반환
boolean containsKey(Object key)|HashMap에 지정된 키가 포함되어있는지 알려줌
boolean containsValue(Object value)|HashMap에 지정된 값이 포함되었는지 알려줌
Set entrySet()|HashMap에 저장된 키와 값을 엔트리의 형태로 Set에 저장해서 반환
Object get(Object key)|지정된 키와 값을 반환<br>키를 못찾으면, 못찾으면 null로 반환
Object getOrDefault(Object key, Object defaultValue)|지정된 키와 값을 반환<br>키를 못찾으면, 기본값으로 지정된 객체를 반환
boolean isEmpty()|HashMap이 비어있는지 알려줌
Set keySet()|HashMap에 저장된 모든 키가 저장된 Set을 반환
Object put(Object key, Object value)|지정돈 키와 값을 HashMap에 저장
void putAll(Map m)|Map에 저장된 모든 요소를 HashMapd에 저장
Object remove(Object key)|HashMap에서 지정된 키로 저장된 값(객체)을 제거
Object replace(Object key, Object oldValue, Object newValue)|지정된 키와 객체가 모두 일치하는 경우에만 새로운 객체로 대체
int size()|HashMap에 저장된 모든 요소의 개수를 반환
Collection values()|HashMap에 저장된 모든 값을 컬렉션의 형태로 반환

# TreeMap

## 1. TreeMap
- 범위 검색과 정렬에 유리한 컬렉션 클래스
- HashMap보다 데이터 추가, 삭제에 시간이 더 걸림(비교하면서 저장하기 때문)
## 2. TreeMap의 메서드
생성자|설명
--|--
TreeMap()|TreeMap객체를 생성
TreeMap(Comparator c)|지정된 Comparator를 기준으로 정렬하는 TreeMap객체을 생성
TreeMap(Map m)|주어진 Map에 저장된 모든 요소를 포함하는 TreeMap을 생성
TreeMap(SortedMap m)|주어진 SortedMap에 저장된 모든 요소를 포함하는 TreeMap을 생성

메서드|설명
--|--
Map.Entry ceilingEntry(Object key)|지정된 key와 일치하거나 큰 것중 제일 작은 것의 키와 값의 쌍(Map.Entry)를 반환. 없으면 null을 반환
Object CeilingKey(Object key)|지정된 key와 일치하거나 큰 것중 제일 작은 것의 키를 반환. 없으면 null을 반환
void clear()|TreeMap에 저장된 모든 객체를 제거
Object clone()|현재 TreeMap을 복제해서 반환
Comparator comparator()|TreeMap의 정렬기준이 되는 Comparator를 반환<br>Comparator가 지정되지 않으면 null을 반환
boolean containsKey(Object key)|TreeMap에 지정된 키가 포함되어있는지 알려줌
boolean containsValue(Object value)|TreeMap에 지정된 값이 포함되어있는지 알려줌
Navigableset descendingKeySet()|TreeMap에 저장된 키를 역순을 정렬해서 NavigableSet에 담아서 반환
Set entrySet()|TreeMap에 저장된 키와 값을 엔트리의 형태로 Set에 저장해서 반환
Map.entry firstEntry()|TreeMap에 저장된 첫번째 (가장 작은) 키와 값의 쌍(Map.Entry)을 반환
Object firstKey()|TreeMap에 저장된 첫번째 키를 반환
Map.Entry floorEntry(Object key)|지정된 key와 일치하거나 작은 것 중에서 제일 큰 키의 쌍을 반환. 없으면 null을 반환
Object floorKey(Object key)|지정된 key와 일치하거나 작은 것 중에서 제일 큰 키의 쌍을 반환. 없으면 null을 반환
Object get(Object key)|지정된 키와 값을 반환
SortedMap headMap(Object toKey)|TreeMap에 저장된 첫번째 요소부터 지정된 범위에 속한 모든 요소가 담기 SortedMap을 반환(toKey는 미포함)
NavigableMap headMap(Object toKey, boolean inclusive)|TreeMap에 저장된 첫번째 요소부터 지정된 범위에 속한 모든 요소가 담긴 SortedMap을 반환.inclusive의 값이 true면 tokey도 포함
Map.Entry higherEntry(Object key)|지정된 키보다 큰 키 중에서 제일 작은 키의 쌍을 반환
Object higherKey(Object key)|지정된 키보다 큰 키 중에서 제일 작은 키의 쌍을 반환
boolean isEmpty()|TreeMap이 비어있는지 알려준다.
Set keySet()|TreeMap에 저장된 모든 키가 저장된 Set을 반환
Map.Entry lastEntry()|TreeMap에 저장된 마지막 키의 쌍을 반환
Object lastKey()|TreeMap에 저장된 마지막 키를 반환
Map.Entry lowerEntry(Object key)|지정된 키보다 작은 키 중에서 제일 큰 키의 쌍을 반환
Object lowerKey(Object key)|지정된 키보다 작은 키 중에서 제일 큰 키의 쌍을 반환
NavigableSet navigableKeySet()|TreeMap의 모든 키가 담긴 NaviableSet을 반환
Map.Entry pollFirstEntry()|TreeMap에서 제일 작은 키를 제거하면서 반환
Map.Entry pollLastEntry()|TreeMap에서 제일 큰 키를 제거하면서 반환
Object put(Object key, Object value)|지정된 키와 값을 TreeMap에 저장
void putAll(Map map)|Map에 저장된 모든 요소를 TreeMap에 저장
Object remove(Object key)|TreeMap에서 지정된 키로 저장된 값(객체)를 제거
Object replace(Object key, Object value)|기존의 키의 값을 지정된 값으로 변경
boolean replace(Object key, Object oldValue, Object newValue)|기존의 키의 값을 새로운 값으로 변경.<br>단, 기존의 값과 지정된 값가 일치해야 한다.
int size()|TreeMap에 저장된 요소의 개수를 반환
NavigableMap subMap(Object fromKey, boolean fromInclusive, Object toKey , boolean toInclusive)|지정된 두 개의 키 사이에 있는 모든 요소들이 담긴 NavigableMap을 반환
SortedMap tailMap(Object fromKey)|지정한 두 개의 키 사이에 있는 모든 요소들이 담긴 SortedMap을 반환
NavigableMap tailMap(Object fromKey, boolean inclusive)|지정된 키부터 마지막 요소의 범위에 속한 요소가 담긴 NavigbaleMap을 반환
Collection values()|TreeMap에 저장된 모든 ㄱ밧을 컬렉션의 형태로 반환

# Collctions
- COllctions는 컬렉션과 관련된 메서드를 제공.
- `java.util.Collection` `인터페이스`
- `java.util.Collections` `클래스`
## 1. 컬렉션의 동기화
- `synchronizedXX()`
- `멀티 쓰레드(mult-thread)` 프로그래밍에서는 하나의 객체를 여러 쓰레드가 동시에 `접근`할 수 있기 때문에 `데이터의 일관성`을 유지하기 위해서 공유되는 객체에 `동기화`가 필요

- `vector와 Hashtable`과 같은 구버젼 클래스들은 자체적으로 동기화처리가 되있지만, 멀티쓰레드 프로그래밍이 아닌 경우에는 불필요한 기능이 되어 성능을 떨어뜨리는 요인이 된다.
- `ArrayList와 HashMap`과 같은 컬렉션은 동기화를 자체적으로 하지 않고, 필요한 경우에 `java.util.Collections`클래스의 동기화 메서드를 이용해서 동기화처리가 가능하게 한다.
- 현대의 프로그래밍 경우 동기화는 필요한 경우에만 해야 한다.
```java
static Collection synchronizedCollection (Collection c)
static List       synchronizedList (List list)
static Set        synchronizedSet (Set s) 
static Map        synchronizedMap (Map m)
static SortedSet  synchronizedSortedSet (SortedSet s)
static SortedMap  synchronizedSortedMap (SortedMap m)
```
```java
// 위의 메서드 사용방법
// 동기화되지 않은 ArrayList를 동기화해서 syncList에 저장
// List syncList는 동기화된 리스트, synchronizedList (new ArrayList(...) 동기화 되지 않은 리스트
List syncList = Collections.synchronizedList (new ArrayList(...));
```

## 2. 변경불가 컬렉션 만들기
- `unmodifiableXX()`
- 컬렉션에 저장된 데이터를 보호하기 위해 컬렉션을 변경할 수 없는 `읽기전용`으로 만들때가 있다.
- 대부분 멀티 쓰레드 프로그래밍에서 여러 쓰레드가 하나의 컬렉션을 공유하다보면 데이터가 손상되는데, 이때 방지하는 메서드이다.
```java
static Collection unmodifiableCollection (Collection c)
static List       unmodifiableList (List list)
static Set        unmodifiableSet (Set s) 
static Map        unmodifiableMap (Map m)
static SortedSet  unmodifiableSortedSet (SortedSet s)
static SortedMap  unmodifiableSortedMap (SortedMap m)
```
## 3. 싱글톤 컬렉션 만들기
- `singleton()`
- 단 하나의 객체만을 저장하는 컬렉션

- 매개변수로 저장할 요소를 지정하면, 해당 요소를 저장하는 컬렉션 반환. 이때, 반환된 컬렉션은 변경 불가
```java
static List singletonList (Object o)
static Set singleton (Object o)         // singletonSet이 아님
static Map singletonMap (Object key, Object value)
```
## 4. 한 종류의 객체만 저장하는 컬렉션 만들기
- `checkedXX()`

- 컬렉션에 지정된 종류의 객체만 저장할 수 있도록 제한하고 싶을 때 사용
```java
static Collection   checkedCollection (Collection c, Class type)
static List         checkedList (List list, Class type)
static Set          checkedSet (Set s, Class type)
static Map          checkedMap (Map m, Class type)
static Queue        checkedQueue (Queue queue, Class type)
static NavigableSet checkedNavigableSet (NavigableSet s, Class type)
static SortedSet    checkedSortedSet (SortedSet s, Class type)
static NavigableMap checkedNavigableMap (NavigableMap m, Class keyType, Class valueType)
static SortedMap    checkedSortedMap (SortedMap m, Class keyType, Class valueType)
```
```java
// 사용방법
// 두 번째 매개변수에 저장할 객체의 클래스를 지정
List list = new ArrayList();
List checkedList = checkedList (List, String.class); // String만 저장가능
checkedList.add("abc");          // ok
checkedList.add(new Integer(3)); // 에러. ClassCastException발생
```

# reference 
자바의 정석 - 남궁성
