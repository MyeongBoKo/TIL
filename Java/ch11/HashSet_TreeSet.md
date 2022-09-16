# HashSet
- 순서X, 중복X


## 1. HashSet
- Set인터페이스를 구현한 대표적인 컬렉션 클래스

- 순서를 유지하려면, LinkedHashSet클래스를 사용
- HashSet은 객체를 저장하기 전에 기존에 같은 객체가 있는지 확인. 이때 같은 객체가 없으면 저장하고, 있으면 저장하지 않는다.
- boolean add(Object o)는 저장할 객체의 equals()와 hashCode()를 호출해서 중복확인을 한다.
- equals()와 hashCode가 오버라이딩 해야 hashSet이 작동한다.

```java
// equals(), hashCode()는 Oject클래스이다. 
class Person {  // Class Person extands Object
    String name;
    int age;

    Person (String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String toString() {
        return name + ":" + age;
    }
}

public boolean equals(Object obj) {
    if (!(obj instanceof Person)) return false;

    Person tmp = (Person)obj;

    return name.equals(tmp.name) && this.age == tmp.age;
}

// old
public int hashCode() {
    return (name+age).hashCode();   // String hashCod 호출
}

// new
public int hashCode() {
    return Objects.hash(name, age)
}
```

## 2. HashSet 메서드
생성자|설명
--|--
Hashset()|HashSet 객체를 생성
HashSet(Collection c)|주어진 컬렉션을 포함하는 HashSet객체를 생성
HashSet(int initialCapacity)|주어진 값을 초기용량으로 하는 HashSet객체를 생성
HashSet(int initialCapacity, float loadFactor)|초기용량과 load factor를 지정하는 생성자

메서드|설명
--|--
boolean add(Object o)|새로운 객체를 저장
boolean addAll(Collection c)|주어진 컬렉션에 저장된 모든 객체들을 추가
void clear()|저장된 모든 객체를 삭제
Object clone()|HashSet을 복제해서 반환(얇은 복사)
boolean contains(Object o)|지정된 객체를 포함하고 있는지 알려준다.
boolena contaninsAll(Collecion c)|주어진 컬렉션에 저장된 모든 객체들을 포함하고 있는지 알려준다.
boolean isEmpty()|HashSet이 비어있는지 알려준다.
boolean iterator()|iterator를 반환한다.
boolean remove(Object o)|지정된 객체를 HashSet에서 삭제
boolean removeAll(Collection)|주어진 컬렉션에 저장된 모든 객체와 동일한 것들을 HashSet에서 삭제
boolean retainAll(Collection)|주어진 컬렉션에 저장된 모든 객체와 동일한 것만 남기고 삭제
int size()|저장된 객체의 개수를 반환
Object[] toArray|저장된 객체들을 객체배열의 형태로 반환
Object[] toArray(Object[] a)|저장된 객체들을 주어진 객체배열(a)에 담는다.


```java
import java.util.*;

class HashSetEx1 {
    public static void main (String[] args) {
        Object[] objArr = {"1", new Integer(1), "2", "2", "3", "3", "4", "4", "4"};
        Set set = new HashSet();

        for (int i = 0; i < objArr.length; i++>) {
            set.add(objArr[i] + "=" + set.add(objArr[i]));
        }

        System.out.println(set.add(objArr[i]));

        // HashSet에 저장된 요소들을 출력한다.
        System.out.println(set);

        // HashSet에 저장된 요소들을 출력(Iterator 이용)
        Iterator it = set.iterator();

        while(it.hasNext()) {   // 1. 읽어올 요소가 있는지 확인
            System.out.println(it.next());  // 2. 요소 하나 꺼내기
        }
    }
}
```

```java
import java.util.*;

class HashSetLotto {
    public static void main(String[] args) {
        Set set = new HashSet();

        for (int i  = 0; set.size() < 6>; i++) {
            int num = (int)(Math.random()*45) + 1;
            // set.add(new Integer(num))
            set.add(num)    // 위의 코드로 컴파일러가 자동 형변환
        }

        System.out.println(set);    // 정렬되지 않은 상태로 출력

        List list = new LinkedList(set);    // LinkedList(Collection c), 1. set의 모든 요소를 List에 저장
        Collections.sort(list);             // Collections.sort(List list), set은 정렬불가 하기 때문에 set -> list, 2. List를 정렬
        System.out.println(list);           // 3. List를 출력
    }
}
```
## 3. TreeSet
- 범위 검색(from ~ to)과 정렬에 유리한 컬렉션 클래스
- HashSet보다 데이터 추가, 삭제에 시간이 더 걸림

### TreeSet - 범위 탐색, 정렬
- 이진 탐색 트리(binary search tree)로 구현. 범위 탐색(from ~ to)과 정렬에 유리
- 이진 트리는 모든 노드가 최대 2개의 하위 노드를 갖음
- 각 요소(node)가 나무형태로 연결(LinkedList의 변형)

### 이진 탐색 트리
- 부모보다 작은 값은 왼쪽, 큰 값은 오른쪽에 저장
- 데이터가 많아질 수록 추가, 삭제에 시간이 더 걸림(비교 횟수 증가)

### TreeSet - 데이터 저장과정 boolean add(Object o)
- add 메서드를 호출하면 add 메서드 내에서 equals()와 hashCode()를 호출한다.
- TreeSet은 중복을 허용하지 않기 때문에 확인을 해야 하기 때문이다. 
- 같은 것이 있으면 저장 실패 false를 반환
- 비교 후 저장

### 트리 순회(tree Traversal)
- 이진 트리의 모든 노드를 한번씩 읽는 것을 트리 순회라고 한다.
- 부모를 먼저 읽는 방식을 전위 순회(preorder)
- 부모를 나중에 읽는 방식을 후위 순회(postorder)
- 부모를 가운데 놓고, 왼쪽 자식 -> 부모 -> 오른쪽 자식 순으로 순회를 중위 순회(inorder)
  - 중위 순회하면 오름차순이 된다.
  - 그래서 TreeSet 정렬과 범위에 유리하다. 트리가 많아질수록 추가, 삭제하는데 시간이 걸리게 된다. 
- 레벨 순회 한 층씩 읽는 방식

# reference
자바의 정석 - 남궁성


