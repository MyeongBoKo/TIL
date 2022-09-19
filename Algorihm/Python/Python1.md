# 숫자형
## 1. 정수형
- Integer. 정수를 뜻하는 자료형
- 양의 정수, 0, 음의 정수
## 2. 실수형
- 소수점이 포함된 숫자
```python
a = 1.2
a = -3.53
```
- 컴퓨터식 지수 표현 방식
```python
a = 4.2E10      //  4.2*10^10
a = 4.24e-10    //  4.24*10^-10
```
## 3. 8진수 16진수
- 8진수를 표현하는 방식 0o or 0O
```python
a = 0o1777
```
- 16진수를 표현하는 방식 0x
```python
a = 0x8ff
b = 0xABC
``` 
## 4. 복소수
- 복소수를 표현할 때 j or J를 사용
```python
a = 1 + 2j
b = 3 - 4J
```
- 복소수 변수 이름 뒤에 '.'를 붙인 다음 함수 이름을 붙여서 복소수 관련 내장 함수 사용
### `복소수.real`: 복소수의 실수 부분 리턴
```python
a = 1 + 2j
a.real
# 1.0
```
### `복소수.imag`: 복소수의 허수 부분을 리턴
```python
a = 1 + 2j
a.imag
#2.0
```
### `복소수.conjuate()`: 복소수의 켤레복소수를 리턴
```python
a = 1 + 2j
a.conjugate()
#(1-2j)
```
### `abs(복소수)`: 복소수의 절댓값을 리턴
```python
a = 1 + 2j
abs(a)
#2.23606797749979
```

## 5. 사칙연산
- (+, -, *, /)
- %: 나눗셈 후 나머지를 반환하는 연산자
- //: 나눗셈 후 소수점 아랫자리를 반환하는 연산자

# 문자열 자료형
- 문자열(Sring)이란 문자, 단어 등으로 구성된 문장들의 집합
- 따옴표로 둘러싸여 있으면 모두 문자열

## 1. 문자열은 만드는 방법
### 1. 큰따옴표(")로 양쪽 둘러싸기
```python
"Hello World"
```
### 2. 작은따옴표(')로 양쪽 둘러싸기
```python
'Hello World'
```
### 3. 큰따옴표(") 3개를 연속(""")으로 써서 양쪽 둘러싸기
```python
"""Life is too short, You need python"""
```
### 4. 작은따옴표(") 3개를 연속(""")으로 써서 양쪽 둘러싸기
```python
'''Life is too short, You need python'''
```

## 2. 문자열 안에 따옴표 나타내기
### 1. 문자열에 작은따옴표 포함
```python
Python's favorite food is perl

# 큰 따옴표 안에 들어 있는 작은 따옴표는 문자열을 나타내기 위한 기호로 인식하지 않는다.
# 이때 작은 따옴표로 묶으면 구문 오류를 발생시킴
food = "Python's favorite food is perl"

```

### 2. 문자열에 큰따옴표 포함
```python
"Python is very easy." he says.

# 큰따옴표를 문장에 나타내고 싶으면 작은따옴표를 이용
say = '"Python is very easy." he says.'
```

### 3. \(백슬래시)를 이용해서 작은따옴표와 큰따옴표를 문장에 포함
- 백슬래시(\)를 작은따옴표 또는 큰따옴표 앞에 삽입하면 뒤의 작은따옴표나 큰따옴표는 문자열을 둘러싸는 기호의 의미가 아닌 문자로 인식한다.
```python
food = 'Python\'s favorie food is perl'
Say = "\"Pyhon is very easy.\" he says"
```
## 3. 여러 줄인 문자열을 변수에 대입하고 싶을 때
### 1. 이스케이프 코드 '\n' 삽입
```python
multiline = "Life is too short\nYou need pyhon"
```

### 2. ''' ~ ''', """ ~ """ 연속된 따옴표 사용
```python
multiline = '''
Life is too short
You need pyhon
'''

multiline = """
Life is too short
You need python
"""
```

## 4. 이스케이프 코드
코드|설명
--|--
`\n`|문자열 안에 줄을 바꿀 때 사용
`\t`|문자열 사에 탭 간격을 줄 때 사용
`\\`|문자\를 그대로 표현할 때 사용
`\'`|작은따옴표를 그대로 표현할 때 사용
`\"`|큰따옴표를 그대로 표현할 때 사용

## 5. 문자열 연산
### 1. 문자열 더해서 연결하기
```python
head = "Python"
tail = " is fun"
head + tail
# Python is fun
```

### 2. 문자열 곱하기
- 문자열에서 *는 문자열의 반복을 의미
```python
a = "Python"
a * 2
# PythonPython
```

## 6. 문자열 인덱싱과 슬라이싱
### 1. 인덱싱
- 인덱싱은 가리킨다는 의미
- 0부터 시작
- 문자열 뒤에서부터 읽기 위해서 (-)기호를 사용
- a[-1]은 맨 뒤의 첫 번째 문자를 말한다.
```python
a = "Life is too short, You need Pyhon"
a[3]
#'e'

a[-1]
# 'n'
```

### 2. 슬라이싱
- a[0:4]은 0부터 4까지의 문자를 뽑아낸다는 뜻
- a[시작번호:마지막번호]를 하면 마지막번호는 포함되지 않는다.
- a[시작번호:] 이렇게 하면 지정한 시작번호에서 그 문자열의 끝까지 뽑아낸다.
- a[:마지막번호] 이렇게 하면 문자열의 처음부터 지정한 마지막번호까지 뽑아낸다.
- a[] 이렇게 하면 문자열의 처음부터 끝까지 뽑아낸다는 의미.
```python
a = "Life is too short, You need Python"
a[0:4]
# 'Life'

a[19:-7]    // 19 ~ -8, (-)로 표현해도 마지마 값은 포함되지 않는다.
# You need
```
```python
a = "20200918Suny"
year = a[:4]        # 처음부터 a[3]
day  = a[4:8]       # a[4] ~ a[7]
weather = a[8:]     # a[8] ~ 끝까지
```
## 7. 문자열 포매팅
- 문자열 내의 특정한 값을 바꿔야 할 경우가 있을 때 이것을 가능하게 해주는 것이 문자열 포매팅이다.
- 문자열 내에 어떤 값을 삽입하는 방법

### 1. 숫자 대입
```python
"I eat %d apples." % 3
# I eat 3 apples.
```
### 2. 문자열 바로 대입
```python
"I eat %s apples. % "three"
"I eat thress apples."
```
### 3. 숫자 값을 나타내는 변수로 대입
```python
number = 3
"I eat %d apples." % number
# I eat 3 apples.
```
### 4. 2개 이상의 값 넣기
```python
number = 10
day = "three"
"I ate %d apples. so I was sick for %s days." %(number, day)
# "I ate 10 apples. so I was sick for three days."
```

### 5. 문자열 포맷 코드   
코드|설명
--|:--:
%s|문자열
%c|문자 1개
%d|정수
%f|부동 소수
%o|8진수
%x|16진수
%%|Literal %(문자 '%', 자체)

## 8. 포맷 코드와 숫자 함께 사용하기
### 1. 정렬과 공백
```python
"%10s" % "hi"
#'        hi'   // 오른쪽 정렬
```
- %10s는 전체 길이가 10개인 문자열 공간에서 hi를 오른쪽 정렬하고, 그 앞의 나머지는 공백으로 남겨두라는 의미

```python
"%-10s" %hi
# 'hi        '    // 왼쪽 정렬
```

### 2. 소수점 정렬
- '.' 뒤의 숫자는 소수점 뒤에 나올 숫자의 개수를 의미
```python
"%0.4f" % 3.1343214789
# '3.1343'

"%10.4f" % 3.314138940
# '    3.3141'  // 전체 길이가 10개인 문자열 공간에서 오른쪽 정렬의미
```

## 문자열 관련 함수

### count(문자의 개수 세기)
```python
a = "hobby"
a.count('b')
# 1
```
### find(위치 알려주기)
- 문자열이 중복하는 경우 앞에 있는 위치로 반환
```python
a = "Python is best choice"
a.find('b')
# 10    // 문자열에서 b가 있는 위치
a.find("k")
# -1    // 문자열에서 존재하지 않으면 -1로 반환

```
### index(위치 알려주기)
- 문자열이 중복하는 경우 앞에 있는 위치로 반환
```python
a = "Life is too short"
a.index('t')
# 8
a.index('k')
# Traceback (most recent call last):
#   File "<pyshell#14>", line 1, in <module>
#     a.index('k')
# ValueError: substring not found
# index의 경우 오류를 발생시킴
```
### join(문자열 삽입)
```python
a = ','
a.join('abcd')
# a,b,c,d
```
### upper(소문자를 대문자로 바꾸기)
```python
a = 'hi'
a.upper()
# 'HI'
```
### lower(대문자를 소문자로 바꾸기)
```python
a = "HI"
a.lower()
# 'hi'
```
### lstrip(왼쪽 공백 지우기)
```python
a = " hi "
a.lstrip()
# "hi "
```
### rstrip(오른쪽 공백 지우기)
```python
a = ' hi '
a.rstrip()
# ' hi'
```
### strip(양쪽 공백 지우기)
```python
a = ' hi '
a.strip()
# 'hi'
```
### replace(문자열 바꾸기)
```python
a = "Life is too short"
a.replace("Life", "Your leg")
```
### split(문자열 나누기)
```python
a = "Life is too short"
a.split()       // 공백을 기준으로 문자열을 나눔
['Life', 'is', 'too', 'short']

a = "a:b:c:d"
a.split(':')    // ':'을 기준으로 문자열을 나눔
['a', 'b', 'c', 'd']
```

# 리스트의 수정, 변경과 삭제
### 1. 리스트에서 하나의 값 수정하기
```python
a = [1, 2, 3]
a[2] = 4
# [1, 2, 4]
```

### 2. 리스트에서 연속된 범위의 값 수정하기
```python
a[1:2]
[2]
a[1:2] = ['a', 'b', 'c']
# a = [1, 'a', 'b', 'c', 4]
```

### 3. [] 사용해서 리스트 요소 삭제
```python
a[1:3] = []
# a= [1, 'c', 4]
```

### 4. del 함수 사용해 리스트 요소 삭제하기
```python
del a[1]
# a = [1, 4]

# del a[x:y]는 x부터 y번째 요소 사이의 값을 제거
```
# 리스트 관련 함수
## 1. append
: .append(x)는 리스트의 맨 마지막에 x를 추가시키는 함수
## 2. sort
: .sort()는 리스트의 요소를 순서대로 정렬

## 3. reverse
: .reverse()는 리스트를 역순으로 뒤집는 함수

## 4. index
: .index(x)는 리스트에 x라는 값이 있으면 x의 위치값을 리턴하는 함수<br>리스트에 없는 값을 리턴하려고 하면 오류발생

## 5. insert
:.insert(a,b)는 리스트의 a번째 위치에 b를 삽입하는 함수

## 6. remove
: .remove(x)는 리스트에서 첫 번째로 나오는 x를 삭제하는 함수

## 7. pop
: .pop()은 리스트의 맨 마지막 요소를 돌려주고, 그 요소는 삭제하는 함수

## 8. count
: .count(x)는 리스트 내에 x가 몇 개 있는지 조사하여 그 개수를 돌려주는 함수

## 9. extend
: .extend(x)는 x에는 리스트만 올 수 있으며 원래의 a 리스트에 x 리스트를 더하는 함수.

# 튜플
- 리스트의 경우 값의 생성, 삭제, 수정이 가능하지만 튜플은 값을 바꿀 수 없다.
- 1개의 요소만을 가질 때 요소 뒤에는 무조건 콤마(,)를 붙여야 한다.   
  ex) t = (1,)

# reference 
점프 투 파이썬 - 박응용
