# 파이썬 내장함수
## abs(x)
- 어떤 숫자를 입력 받았을 때, 그 숫자의 절대값을 돌려주는 함수
  
## all(x)
- 반복 가능한 자료형(리스트, 튜플, 문자열, 딕셔너리, 집합 등 for 문으로 그 값을 출력할 수 있는 자료형을 말함.) x를 입력 인수로 받으며, 이 x가 모두 참이면 True, 거짓이 하나라도 있으면 False를 리턴

## any(x)
- x 중 하나라도 참이 있을 경우 True 리턴, x가 모두 거짓일 경우에만 False를 리턴
  
## chr(i)
- 아스키 코드값을 입력 받아 그 코드에 해당하는 문자를 출력

## dir
- 객체가 자체적으로 가지고 있는 변수나 함수를 보여 준다.

## divmod
- divmod(a, b)는 2개의 숫자를 입력을 받고, a를 b로 나눈 몫과 나머지를 튜플 형태로 리턴하는 함수

## enumerate
- 순서가 있는 자료형(리스트, 튜플, 문자열)을 입력으로 받아 인덱스 값을 포함하는 enumerate객체를 리턴
```python
for i, name in enunerate(['body', 'foo', 'bar']):
    print(i, name)

0 bady
1 foo
2 bar
```

## eval
- eval(expression)은 실행 가능한 문자열(1+2, 'hi', 'a' 같은 것)을 입력으로 받아 문자열을 실행한 결과값을 리턴하는 함수
- 파이썬 함수나 클래스를 동적으로 실행하고 싶은 경우에 사용
```python
eval('1+2')
3
eval("'hi' + 'a'")
'hia'
eval('divmod(4, 3)')
(1, 1)
```

## filter
- 첫 번째 인수로 함수 이름을, 두 번째 인수로 그 함수에 차례로 들어갈 반복 가능한 자료형을 받는다.
- 두 번째 인수인 반복 가능한 자료형 요소들이 첫 번째 인수인 함수에 입력되었을 때 리턴값이 참인 것만 묶어서 돌려준다.
```python
def positive(x):
    return x > 0

print(list(filtet(positive, [1, -3, 2, 0, -5, 6])))

# [1, 2, 6]
```

## hex(x)
- 정수값을 입력받아 16진수로 변환하여 리턴하는 함수
```python
hex(234)
'0xea'

hex(3)
'0x3'
```

## id(object)
- 객체를 입력받아 객체의 고유 주소 값(레퍼런스)을 리턴하는 함수
```python
a = 3
id(3)
xxxxxxxx # 주소 값
id(a)
xxxxxxxx

b = a
id(b)
xxxxxxxx

# 3, a, b 모두 같은 객체를 가리킨다.
```

## input
- input([prompt])은 사용자 입력을 받는 함수
- 입력 인수를 문자열로 출력
- [] 기호는 괄호 한의 내용을 생략할 수 있다는 관례적인 표기법
```python
a = input()
hi
a
'hi'

b = input("Enter")  # Enter: 라는 프롬프트를 띄우고 사용자 입력을 받음
```

## int
- int(x)는 문자열 형태의 숫자나 소수점이 있는 숫자 등을 정수 형태로 리턴하는 함수
- 정수를 입력으로 받으면 그대로 리턴
- int(x, radix)는 radix 진수로 표현된 문자열 x를 10진수로 리턴
```python
int('3')
3

int(3.4)
3

int('11', 2)    // 2진수
3

int('1A', 16)   // 16진수
26
```

## isinstance
- `isinstance(object, class)`는 `첫 번째 인수로 인스턴스`, `두 번째 인수로 클래스 이름`을 받음.
- 입력으로 받은 인스턴스가 그 클래스의 인스턴스인지를 판단하여 참이면 True, 거짓이면 False를 반환
```python
class Person: pass  # 아무 기능없는 Person 클래스 생성
...

a = Person()        # Person 클래스의 인스턴스 a 생성
isinstance(a, Person)   # a가 Person 클래스의 인스턴스인지 확인
# True
```

## lambda
- 함수를 생성할 때 사용하는 예약어로써 def와 동일한 기능을 한다.   
`lambda 인수1, 인수2, ... : 인수를 이용한 표현식`

## len
- `입력값의 길이(요소의 전체 개수)`를 리턴하는 함수
```python
len("java")
4
```

## list(s)
- 반복 가능한 자료형 s를 입력받아 `리스트로 만드는 함수`
```python
list("java")
["j", "a", "v", "a"]

a = [3, 6, 9]
b = list(a)
b
[3, 6, 9]
```

## map(f, iterable)
- `함수(f)와 반복 가능한(literable) 자료형`을 입력받음
- map은 입력 받은 자료형의 각 요소가 함수 f에 의해 수행된 결과를 묶어서 리턴하는 함수

## max
- max()는 인수로 반복 가능한 자료형을 입력받아 그 최대값을 리턴하는 함수
```python
max([3, 6, 9])
9

max("abcd")
d
```

## min
- min()는 인수로 반복 가능한 자료형을 입력받아 그 최소값을 리턴하는 함수 

## oct
- 정수 형태의 숫자를 8진수 문자열로 바꾸어 리턴하는 함수

## open
- open(filename, [mode])

## ord
- ord(c)는 문자의 아스키 코드값을 리턴하는 함수

## pow
- pow(x, y)는 x의 y 제곱한 결과값을 리턴하는 함수
```python
pow(2,2)
4

pow(4,2)
16
```

## range

## sorted
- sorted() 함수는 입력값을 정렬한 후 그 결과를 리스트로 리턴하는 함수
```python
sorted([9, 6, 3])
[3, 6, 9]

sorted(['c', 'd', 'a'])
['a', 'c', 'd']
```

## str
- str(object)은 문자열 형태로 객체를 변환하여 리턴하는 함수
```python
str(123)
'123'
str('abc')
'abc'
str('hi'.upper())
'HI'
```

## tuple
- tuple() 반복 가능한 자료형을 입력받아 튜플 형태로 바꿔서 리턴하는 함수
- 튜플이 입력되면 그대로 리턴
```python
tuple("bcd")
('b', 'c', 'd')

tuple([3, 6, 9])
(3, 6, 9)

tuple((3, 6, 9))
(3, 6, 9)
```

## type
- type(object)은 입력값의 자료형이 무엇인지 알려주는 함수
```python
type("apple")
<class 'str'>

type([])
<class 'list'>

type(open("test", w))
<class'_io.TextlOWrapper>

```

## zip
- zip은 동일한 개수로 이루어진 자료형을 묶어 주는 역할을 하는 함수
```python
list(zip([2, 4, 6], [3, 6, 9]))
[(2, 3), (4, 6), (6, 9)]

list(zip([1, 3, 5], [2, 4, 6], [3, 6, 9]))
[(1, 2, 3), (3, 4, 6), (5, 6, 9)]

list(zip("java", "pyth"))
[('j', 'p'), ('a', 'y'), ('v', 't'), ('a', 'h')]
```

# reference
점프 투 파이썬 - 박응용
