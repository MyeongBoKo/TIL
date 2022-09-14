# ArrayList
## ArrayList란
1. 기존의 Vector를 개선한 것을 Vector와 구현원리리와 기능적인 측면에서 동일하다고 볼 수 있다.

2. Vector는 동기화O, ArrayList는 동기화x, 즉 현재의 프로그래밍은 동기화가 필요하면 동기화를 해주는 메서드를 이용해서 동기화 시켜서 성능을 높인다.
3. List 인터페이스를 구현하기 때문에 데이터의 저장순서가 유지되고, 중복을 허용한다.
4. 객체의 저장공간으로 배열을 사용한다.
5. Object가 배열의 타입의 최고 조상이기 때문에 모든 종류의 객체를 담을 수 있다.
6. 배열에 더 이상 저장할 공간이 없다면 보다 큰 새로운 배열을 생성해서 기존의 배열에 저장된 내용을 새로운 배열로 복사한 다음에 저장한다.

## ArrayList 메서드
생성자|설명
--|--
ArrayList()| 크기가 10인 ArrayList 생성, 기본생성자
ArrayLsit(Collection)|주어진 컬렉션이 저장된 ArrayList를 생성
ArrayList(int initialCapacity)|지정된 초기용량을 갖는 ArrayList를 생성

메서드(추가)|설명
--|--
boolean add(object o)|ArrayList의 마지막에 객체를 추가, 성공하면 True
void add(int index, Object element)|지정된 위치에 객체를 저장
boolean addAll(Collection c)|주어진 컬렉션의 모든 객체를 저장
boolean addAll(int inedx, Collection c)|지정된 위치로부터 주어진 컬렉션의 모든 객체를 저장

메서드(삭제)|설명
--|--
void clear()|ArrayList를 완전히 삭제
Object remove(int index)|지정된 위치에 있는 객체를 삭제
boolean remove(Object o)|지정한 객체를 삭제(성공 True, 실패 False)
boolean removAll(Collection c)|지정한 컬렉션에 저장된 것과 동일한 객체들을 ArrayList에서 삭제
boolean retainAll(Collection c)|ArrayList에 저장된 객체 중에서 주어지 컬렉션과 공통된 것을 남기고 나머지는 삭제

메서드(검색)|설명
--|--
boolean contains(Obect o)|지정된 객체가 ArrayList에 포함되어 있는지 확인
Object get(int index)|지정한 위치에 저장된 객체를 반환
int indexOf(Object o)|지정된 객체가 저장된 위치를 찾아 반환(->)
int lastindexOf(Object o)|지정된 객체가 저장된 위치를 찾아 반환(<-)
Object set(int index, Object element)|주어진 객체를 지정된 위치에 저장

메서드|설명
--|--
Object clone()|ArrayList를 복제
void ensureCapacity(int minCapacity)|ArrayList의 용량을 최소한 minCapacity가 되도록 한다.
Iterator iterator()|ArrayList의 iterator객체를 반환
ListIterator listiterator()|ArrayList의 ListIterator를 반환
ListIterator listiterator(int index)|ArrayList의 지정된 위치로부터 시작하는 ListIterator를 반환
int size()|ArrayList에 저장된 객체의 개수를 반환
void sort(Comparactor c)|지정된 정렬기준(c)로 ArrayList를 정렬
List subList(int fromindex, int toindex)|fromindex ~ toindex사이에 저장된 객체를 반환<br> 이때 객체를 반환할 때 새로운 리스트를 만들어서 반환
Object[] toArray()|ArrayList에 저장된 모든 객체들을 객체배열로 반환
object[] toArray(Object[] a)|ArrayList에 저장된 모든 객체들을 객체배열 a로 담아서 반환
void trimToSize()|용량을 크기에 맞게 줄인다.(빈 공간을 없앤다.)


## ArrayList에 저장된 객체의 삭제과정
ArrayList|데이터 값
:--:|:--:
data[0]|0
data[1]|1
data[2]|2
data[3]|3
data[4]|4
data[5]|null
data[6]|null
#### ArrayList에 저장된 세 번째 데이터(data[2])를 삭제하는 과정. 
1. list.remove(2);를 호출. 이때 list.remove(2)는 인덱스가 2인 객체를 삭제
2. 삭제할 데이터 아래의 데이터를 한 칸씩 위로 복사해서 삭제할 데이터를 덮어쓴다.<br>        

ArrayList|데이터 값
--:|:--:
data[0]|0
data[1]|1
data[2]|3
data[3]|4
data[4]|4
data[5]|null
data[6]|null 

3. 데이터가 모두 한 칸씩 이동했으므로 마지막 데이터는 null로 변경한다.

#### ArrayList에 저장된 세 번째 데이터(data[2])를 삭제하는 과정
- 위로 복사해주면 된다.

## ArrayList의 장단점
- 장점:<br>
1. 배열은 구조가 간단하고, 데이터를 읽는 데 걸리는 시간(접근시간, access time)
이 짧다<br>index가 n인 데이터의 주소 = 배열의 주소 + n * 데이터 타입의 크기
- 단점:<br>
1. 크기를 변경할 수 없다.(실행 중에 바꿀 수 없다.)   
     - 크기를 변경해야 하는 경우 새로운 배열을 생성 후 데이터를 복사해야함.
     - 크기 변경을 피하기 위해 충분히 큰 배열을 생성하면, 메모리가 낭비된다.
2. 비순차적인 데이터의 추가, 삭제에 시간이 많이 걸린다.
    - 데이터를 추가하거나 삭제하기 위해, 다른 데이터를 옮겨야 한다.
    - 그러나 순차적인 데이터 추가(끝에 추가)와 삭제(끝부터 삭제)는 빠르다.   

# reference 
자바의 정석 - 남궁성
