# 자료형
## 수 자료형
- 코딩 테스트에서 가장 기본적인 자료형
- 데이터는 모든 수로 표현할 수 있다. 
- 일반적으로 정수와 실수를 많이 사용하는데, 정수를 기본으로 사용한다.
- 코딩 테스트에서 대부분 정수형을 다룬다.

## 정수형(Integer)
- 정수를 다루는 자료형
- 종류에는 양의 정수, 0, 음의 정수있다.
- 코딩 테스트에서 출제되는 알고리즘 문제는 대부분 입력과 출력 데이터가 정수형이다.
```python
#양의 정수
a = 10
print(a)

#음의 정수
b = -11
print(b)

#0
c = 0
print(c)
```

## 실수형(Real Number)
- 소수점 아래의 데이터를 포함하는 수 자료형
- 변수에 소수점을 붙인 수를 대입하면 실수형 변수로 처리한다.
- 소수부가 0 또는 정수부가 0인 소수는 0을 생략해서 작성할 수 있다.
```python
# 양의 실수
a = 157.99
print(a)

#음의 실수
b = -993.2
print(b)

# 소수부가 0일 때 0을 생략
c = 8123.
print(c)

# 정수부가 0일 때 0을 생략
d = -.313
print(d)
```
- e나 E를 이용한 지수 표현 방식
  - e는 다음에 오는 수는 10의 지수부를 의미
  - 유효숫자e^지수 = 유효숫자X10^지수
  - 최단 경로 문제에서 도달 할 수 없는 노드에 대하여 최단 거리를 무한을 설정하는데, 이때 최대값이 10억이면 10억을 지수로 표현할 수 있다.
  - 일일이 특정 수를 코드에 입력하기 보다는 지수로 표현하는 것이 실수를 적게 할 확률이 높다.
  - 특정 값이 10억과 유사하면 1e9로 표현할 수 있다.
```python
# 10억의 지수 표현 방식
a = 10e9
print(a)

#1994.0
b = 1.994e3
print(b)

#7.771
c = 7771e-3
print(c)
```
- 컴퓨터는 수 데이터를 처리할 때 2진수를 이용한다.
- 이때 실수 처리할 때 부동소수점 방식을 이용하는데, 실수형을 저장하기 위해 4바이트 혹은 8바이트 고정된 크기를 메모리에 할당하기 때문에 실수 정보를 표현하는데 정확도에 한계가 존재한다.
- 2진수에서는 0.9를 정확히 표현할 수 있는 방법이 없다.
- 컴퓨터가 실수를 정확히 표현하지 못한다는 사실은 기억해야 한다.
```python
a = 0.3 + 0.6
print(a)

if a == 0.9:
  print(True)
else:
  print(False)

#0.8999999999999999
#False
```
- 소수점 값을 비교하는 작업이 필요한 문제일 경우, round() 함수를 이용한다.
- round() 함수를 호출할 때 인자를 넣는데, 첫 번째 인자는 실수형 데이터, 두 번째 인자는 반올림하고자 하는 위치 - 1 이다.
- 두 번째 인자를 넣지 않으면 소수점 첫째 자리에서 반올림한다.
```python
a = 0.3 + 0.6
print(round(a, 4))

if round(a, 4) == 0.9:
  print(True)
else:
  print(False) 

#0.9
#True
```

## 수 자료형의 연산
```python
a = 6
b = 4

# 나누기(파이썬에서는 나눠진 결과는 기본적으로 실수형으로 처리)
print(a / b)

# 나머지
print(a % b)

# 몫
print(a // b)

#거듭제곱(a**b = a^b)
print(a**b)

#1.5
#2
#1
#1296
```

## 리스트 자료형
- 여러 개의 데이터를 연속적으로 담아 처리하기 위해 사용되고, 리스트 대신 배열 혹은 테이블이라고 부르기도 한다.

### 1. 리스트 만들기
- 대괄호([]) 안에 원소를 넣어 초기화한다.
- 쉼표(,)로 원소를 구분한다.
- 비어있는 리스트를 선언할 때는 list() or 대괄호([])를 이용한다.

### 2. 리스트 이용하기
- 리스트의 원소에 접근할 때는 인덱스 값을 괄호 안에 넣는다.
- 인덱스는 0부터 시작한다.
```python
a = [1,2,3,4,5,6,7,8,9]
print(a)

# 인덱스 5, 여섯 번째 원소에 접근
print(a[5])

# 빈 리스트 선언 1)
b = list()
print(b)

# 빈 리스트 선언 2)
c = []
print(c)

#[1, 2, 3, 4, 5, 6, 7, 8, 9]
#6
#[]
#[]
```
- 크기가 N인 1차원 리스트 초기화 방법
```python
n = 10
a = [0]*n
print(a)
#[0, 0, 0, 0, 0, 0, 0, 0, 0, 0]

n = 9
a = []*n
print(a)
#[]
```

### 3. 리스트의 인덱싱과 슬라이싱
- 인덱싱은 인덱스 값을 입력하여 리스트의 특정한 원소에 접근하는 것을 말한다.
- 파이썬에서는 양의 정수, 음의 정수, 0 모두 사용 가능하다.
- 음의 정수를 입력하면 원소를 거꾸로 탐색한다.
- -1을 입력하면 가장 마지막 원소가 출력된다.
```python
a = [1, 2, 3, 4, 5, 6, 7, 8, 9]

# -1을 이용
print(a[-1])

# 뒤에서 세 번째 원소 출력
print(a[-3])

# 세 번째 원소 변경
print(a[2])
a[2] = 1
print(a[2])

#9
#7
#3
#1
```
- 슬라이싱은 연속적인 위치를 갖는 원소들을 가져와야 할 때 이용한다.
- 대괄호 안에 콜론(:)을 넣어서 시작 인데스와 끝 인덱스를 설정한다.
- 인덱스는 0부터 시작하고, 끝 인덱스는 포함하지 않는다.
```python
a = [1, 2, 3, 4, 5, 6, 7, 8, 9]

print(a[:])

print(a[1:3])

print(a[2:])

print(a[:5])

#[1, 2, 3, 4, 5, 6, 7, 8, 9]
#[2, 3]
#[3, 4, 5, 6, 7, 8, 9]
#[1, 2, 3, 4, 5]
```

### 리스트의 컴프리헨션
- 대괄호 안에 조건문과 반복문을 넣는 방식으로 리스트를 초기화 할 수 있다.
- 리스트의 컴프리헨션을 이용하면 소스코드를 간결하게 작성할 수 있다
```python
#홀수 호출하기
# 리스트의 컴프리헨션 이용 O
array = [i for i in range(20) if i % 2 == 1]

print(array)

# 리스트의 컴프리헨션 이용 X
array = []
for i in range(20):
  if i % 2 == 1:
    array.append(i)

print(array)

#[1, 3, 5, 7, 9, 11, 13, 15, 17, 19]
#[1, 3, 5, 7, 9, 11, 13, 15, 17, 19]
```

```python
#제곱 값 호출하기
# 리스트의 컴프리헨션 이용 O
array = [i*i for i in range(10)]
print(array)

# 리스트의 컴프리헨션 이용 X
array = []
for i in range(10):
  array.append(i*i)

print(array)

#[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
#[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```
- 리스트 컴프리헨션을 이용한 2차원 리스트 초기화
```python
# N X M = 3 X 4
n = 3
m = 4
array = [[0] * m for _ in range(n) ]
print(array)

array = []
for _ in range(n):
  array.append([0]*m)

print(array)

#[[0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]]
#[[0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]]
```

- 언더바(_)는 반복을 수행하되 반복을 위한 변수의 값을 무시하고자 할 때 사용한다.
```python
summary = 0
for i in range(1, 10):
  summary += i
print(summary)

#45

for _ in range(5):
  print("Hello World")

#Hello World
#Hello World
#Hello World
#Hello World
#Hello World
``` 
- 특정 크기의 2차원 리스트를 초기화할 때는 반드시 리스트 컴프리헨션을 사용해야 한다.
- 내부적으로 포함된 3개의 리스트가 모두 동일한 객체에 대한 3개의 레퍼런스로 인식되기 때문이다.

```python
n = 3
m = 4
array = [[0]*m] * n
print(array)

array[1][1] = 5
print(array)

#[[0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]]
#[[0, 5, 0, 0], [0, 5, 0, 0], [0, 5, 0, 0]]
```

### 리스트 관련 기타 메서드
메서드명 | 사용법 | 설명 | 시간 복잡도
--|--|--|--
append()|변수명.append()|리스트에 원소를 하나 삽입할 때 사용한다.|O(1)
sort()|변수명.sort()|기본 정렬 기능으로 오름차순으로 정렬한다.|O(NlogN)
sort()|변수명.sort(reverse=True)|내림차순으로 정렬한다.|O(NlogN)
reverse()|변수명.reverst()|리스트의 원소의 순서를 모두 뒤집어 놓는다.|O(N)
insert()|변수명.insert(삽입할 위치 인덱스, 삽입할 값)|특정한 인덱스 위치에 원소를 삽입할 때 사용한다.|O(N)
count()|변수명.count(특정 값)|리스트에서 특정한 값을 가지는 데이터의 개수를 셀 때 사용한다.|O(N)
remove()|변수명.remove(특정 값)|특정한 값을 갖는 원소를 제거하는데, 값을가진 원소가 여러 개면 하나만 제거한다.|O(N)

- insert(), remove()는 데이터를 삽입 또는 삭제한 후에 리스트의 원소 위치를 조정해야 하기 때문에 수행하는데 시간이 걸린다.
- insert() 대신 append()를 사용하고, remove()는 다음과 같이 사용해야 한다.

```python
a = [1, 2, 3, 4, 5, 6, 7, 8, 9]
remove_set = [3, 5]

result = [i for i in a if i not in remove_set]  # a 부분에 포함되어 있지 않았을 때만 리스트 변수인 result에 넣겠다
print(result)
```

## 문자열 자료형
### 문자열 초기화
- 큰따옴표로 구성하는 경우, 내부적으로 작은따옴표를 포함가능
- 작은따옴표로 구성하는 경우, 내부적으로 큰따옴표를 포함가능
- (\)를 사용하면, 큰따옴표와 작은따옴표를 문자열에 포함시킬 수 있다.
```python
data = "You don't give up \"python\""
print(data)

#data = "You don't give up \"python\""
```
### 문자열 연산
```python
a = "Hello"
b = "world"
print(a +" "+b)
#Hello world

a = "String"
print(a*5)
#StringStringStringStringString
```
- 문자열은 내부적으로 리스트와 같이 처리되기 때문에 인덱싱과 슬라이싱이 가능하다.
```python
a = "Study"
print(a[1:])
#tudy

print(a[2])
#u
```

## 튜플 자료형
- 튜플 자료형은 리스트와 매우 유사하다.
- 한 번 선언된 값을 변경할 수 없다.
- 소괄호를 이용한다.
```python
a = (1, 2, 3, 4)
print(a)

#(1, 2, 3, 4)
a[2] = 7

# TypeError                                 Traceback (most recent call last)
# <ipython-input-2-fa3b14a6dfc1> in <module>
#       2 print(a)
#       3 
# ----> 4 a[2] = 7

# TypeError: 'tuple' object does not support item assignment
```
-  즉, 대입 연산자를 사용하여 값을 변경할 수 없다.
-  다익스트라 최단 경로 알고리즘의 경우 최단 경로를 찾아주는 알고리즘 내부에서는 우선순위 큐를 이용하는데 해당 알고리즘에서 우선순위 큐에 한 번 들어간 값은 변경하지 않는다. 그래서 튜플의 성질을 이용해서 튜플로 구성하여 소스코드를 작성한다.

## 사전 자료형
- 키와 값의 쌍을 데이터로 가지는 자료형이다.

키(Key)|값(Value)
--|--
사과|Apple
바나나|Banana
오렌지|Orange

```python
data = dict()
data['사과'] = 'Apple'
data['바나나'] = 'Banana'
data['오렌지'] = 'Orange'

print(data)

if '사과' in data:
  print("데이터에 사과를 가진 키가 있습니다.")
```

### 사전 자료형 관련 함수
- Keys()<br>
  :키 데이터만 뽑아서 리스트로 이용할 때 사용하는 함수
- Values()<br>
  :값 데이터만 뽑아서 리스트로 이용할 때 사용하는 함수
```python
# 키 데이터만 담은 리스트
key_list = data.keys()

# 값 데이터만 담은 리스트
value_list = data.values()

print(key_list)
print(value_list)

# 각 키에 따른 값을 하나씨 출력
for key in key_list:
  print(data[key])
```

## 집합 자료형
- 파이썬은 집합(set)을 처리하기 위한 집한 자료형을 제공한다. 집합은 기본적으로 리스트 or 문자열을 이용해서 만들 수 있다.
  - 중복을 허용하지 않는다.
  - 순서가 없다.
- 순서가 없기 때문에 인덱싱으로 값을 얻을 수 없다.
- 값 데이터로 이루어져 있다.
```python
# 집합 자료형 초기화 방법 1)
data = set([1, 1, 2, 3, 4, 4, 5])
print(data)

# 집합 자료형 초기화 방법 2)
data = {1, 1, 2, 2, 3, 4, 4, 5}
print(data)
```

### 집합 자료형의 연산

- 합집합 연산 시 '|' 사용
- 교집합 연산 시 '&' 사용
- 차집합 연산 시 '-' 사용
```python
a = set([1,2,3,4,5])
b = set([3,4,5,6,7])

print(a | b) # 합집합
print(a & b) # 교집합
print(a - b) # 차집합
```
### 집합 자료형 관련 함수
- add()<br>
  :하나의 집합 데이터에 값을 추가할 때 사용
- update()<br>
  :여러 개의 값을 한꺼번에 추가할 때 사용
- remove()<br>
  :특정한 값을 제거할 때 사용
```python
data = set([1,2,3])
print(data)

data.add(4)
print(data)

data.update([5, 6])
print(data)

data.remove(3)
print(data)
```
# reference
## *이것이 코딩 테스트다 - 나동빈*에서 **발췌한 내용**을 인용했습니다.
