# Array
## Array란
- 배열을 다루기 편리한 메서드(static) 제공

### 배열의 출력
- toString()

### 배열의 복사
- copyOf()
- copyOfRange()

### 배열 채우기
- copyOf()
- fill()
- setAll()

### 배열의 정렬과 검색
- sort()
- binarySearch() 

### 순차 검색(탐색)과 이진 검색
순차검색:
- 순차 검색(탐색)은 순서대로 찾는 것을 의미
- 앞에서부터 찾는 것을 말한다.<br>
이진검색:
- 정렬을 한 후에 반으로 자른 후에 내가 찾고자 하는 수와 비교한다. 이 행위를 반복해서 내가 구하고자 하는 값의 위치를 찾는 방법
- 무조건 정렬을 한 후에 해야 한다.
- 정렬의 속도를 높이는 것이 중요하다.

### 배열의 비교와 출력
- equals()
- toString()

### 다차원 배열의 출력 - deepToString()
- int[] arr = {0, 1, 2, 3, 4};  // 1차원
- int[][] arr2D = {{11, 12}, {21, 22}};     // 2차원
- System.out.println(Array.toString(arr));  // [0, 1, 2, 3, 4]
- System.out.println(Array.deeptoString(arr2D));    // [[11, 12], [21, 22]]

### 다차원 배열의 비교 - deepEquals()
- String[][] str2D = new String[][] {{"aaa", "bbb"}, {"AAA", "BBB"}};
- String[][] str2D2 = new String[][] {{"aaa", "bbb"}, {"AAA", "BBB"}};
- System.out.println(Arrays.equals(str2D, str2D));      // false
- System.out.println(Arrays.deepEquals(str2D, str2D));  // true

### 배열을 List로 변환 
- asList(Object... a) - 읽기 전용

# reference 
자바의 정석 - 남궁성

  
