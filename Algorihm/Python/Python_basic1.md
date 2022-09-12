## 숫자 자료형
```python
print(5)     ## 양수
print(-10)   ## 음수
print(3.14)  ## 실수
print(1000)  ## 큰 수
print(5+3)   ## 덧셈 연산
print(2*8)   ## 곱셈 연산   
print(3*(3+1)) ## 복잡한 연산
```

## 문자열 자료형('str', "str")
```python
print('풍선') 
print("나비")
print("zzzzz")
print("z"*5)
```
## boolean 자료형(참과 거짓을 표현하는 자료형)
```python
참 / 거짓
print( 5 > 10)  # False
print( 5 < 10)  # True
print(True)
print(False)
print(not True) # not은 뒤에 있는 무언가의 반대를 의미한다.
print(not False)
print(not (5 > 10)) 
```

## 변수 variable
1. 애완동물을 소개해 주세요~
2. print("우리집 강아지의 이름은 연탕이예요")
3. print("연탄이는 4살이며, 산책을 아주 좋아해요")
4. print("연탄이는 어른일까요? True")
- 이때 강아지의 이름이 바뀐다면 모든 문장을 수정해야 한다.
- 변수는 어떤 값을 저장하는 공간이라고 생각하면 된다.
```python
animal = "강아지"
name = "연탄이"
age = 4             # 정수형의 경우 문자형으로 쓰기 위해서는 str형변화 시켜야 한다.
hobby = "산책"
is_adult = age >= 3 # boolean도 문자형으로 쓰기 위해서 str로 형변환 시켜야 헌더,

print("우리집 " + animal + "의 이름은 " + name + "예요")

hobby = "공놀이"    # 문장 중간에 변수 선언 가능하다.
print(name + "는 "+ str(age) +"살이며, "+ hobby +"를(을) 아주 좋아해요")
print(name, "는 ", age ,"살이며, ", hobby ,"를(을) 아주 좋아해요")     # (,)를 사용하면, 정수형과 boolean의 경우 형변환 하지 않아도 실행된다. 이떄 (,)를 사용하면 띄어쓰기 한칸이 무조건 포함
print(name + "는 어른일까요? " + str(is_adult))
```
## 주석
- 우리 프로그램 코드 내에 포함되어 있지만, 실제로 실행되지 않는 문장이다. 
주석을 사용하는 방법
1. (#)을 사용해서 한 문장을 주석처리한다.
2. (''' ~ ''')을 사용해서 여러 문장을 주석처리한다.


## Quiz) 변수를 이용하여 다음 문장을 출력하시오
```
변수명
: Station

변수값
: "사당", "신도림", "인천공항" 순서대로 입력

출력 문장
: xx 행 열차가 들어오고 있습니다.
```
```python
Station = "인천공항"
print(Station +"행 열차가 들어오고 있습니다.")

 Station1 = "사당"
 Station2 = "신도림"
 Station3 = "인천공항"

 print(Station1 + " 행 열차가 들어오고 있습니다.")
 print(Station2 + " 행 열차가 들어오고 있습니다.")
 print(Station3 + " 행 열차가 들어오고 있습니다.")

 print(Station1, "행 열차가 들어오고 있습니다.")
 print(Station2, "행 열차가 들어오고 있습니다.")
 print(Station3, "행 열차가 들어오고 있습니다.")
 ```

## 연산자
```python
print(1+1)  # 2
print(3-2)  # 1
print(5*2)  # 10
print(6/3)  # 2

print(2**3) # 2^3 = 8
print(5%3)  # %는 나머지 구하는 연산자, 5%3=2
print(10%3) # 10%3 = 1
print(5//3) # //을 구하는 연산자, 5//3 = 1
print(10//3)# 10//3 = 3

print(10 > 3)   # True
print(4 >= 7)   # False
print(10 < 3)   # False
print(5 <= 5)   # True

print(3 == 3)   # == 등호기준으로 좌변 우변의 값이 똑같은지 확인하는 연산자이다. True
print(4 == 2)   # False
print(3 + 4 == 7)   # Ture

print(1 != 3)      # != 등호기준으로 좌변 우변의 값이 다른지를 확인하는 연산자이다. True
print(not(1 != 3)) # False, not은 not 뒤에 나오는 값을 부정해주는 연산자이기 때문에 False라는 값이 출력

# 그리고(and, &) - 조건이 모두 만족해야 True가 출력
print((3 > 0 ) and ( 3 < 5))    # True
print((3 > 0 ) & ( 3 < 5))      # True

# 또는(or, |) - 조건 하나만이라도 만족하면 True가 출력
print((3 > 0 ) or ( 3 > 5))    # True
print((3 > 0 ) | ( 3 > 5))    # True

# 연속적인 값도 표현 가능하다.
print(5 > 4 > 3)    # True
print(5 > 4 > 7)    # False

# 간단한 수식
print(2 + 3 * 4)
print((2 + 3) * 4) # 우선순위 연산
number = 2 + 3 * 4
print(number)   # 14

number = number + 2
print(number)   # 16

number += 2 #number = number + 2
number *= 2 #number = number * 2
number /= 2 #number = number / 2
number -= 2 #number = number - 2
number %= 2 #number = number % 2
```

## 숫자처리 함수
- abs(-a)   # (-a)안에 있는 값의 절대값을 의미
- pow(a, b) # a^b을 의미
- max(a, b) # a, b 중에서 최대값을 반환한다.
- min(a, b) # a, b 중에서 최소값을 반환한다.
- round()   # 반올림하는 메서드, 이때 소수 점 첫째자리에서 반올리이 이루어짐
```python
from math import *   # math library를 사용하겠다는 의미
print(floor(4.99))  # 내림
print(ceil(3.14))   # 올림
print(sqrt(16))     # 제곱근
```
## 랜덤함수(난수)
```python
from random import *

print(random())     # 0.0 ~ 1.0 미만의 임의의 값 생성
print(random() * 10)    # 0.0 ~ 10.0 미만의 임의의 값 생성
print(int(random() * 10)) # 0 ~ 10 미만의 임의의 값 생성
print(int(random() * 10) + 1) # 1 ~ 11 미만의 임의의 값 생성

print(int(random() * 45) + 1)
print(int(random() * 45) + 1)
print(int(random() * 45) + 1)
print(int(random() * 45) + 1)
print(int(random() * 45) + 1)

print(randrange(1, 46)) # 1 ~ 46 미만의 임의의 값 생성

print(randint(1, 45))     # 1 ~ 45 이하의 임의의 값 생성 이때, 45포함
```


## Quiz) 
```
당신은 최근에 코딩 스터디 모임을 새로 만들었습니다.
월 4회 스터디를 하는데 3번은 온라인으로 하고 1번은 오프라인으로 하기로 했습니다.
아래 조건에 맞는 오프라인 모임 날짜를 정해주는 프로그램을 작성하시오.

조건1 : 랜덤으로 날짜를 뽑아야 함
조건2 : 월별 날짜는 다름을 감안하여 최소 일수인 28 이내로 정함
조건3 : 매월 1~3일은 스터디 준비를 해야 하므로 제외

(출력문 예제)
오프라인 스터디 모임 날짜는 매월 x 일로 선정되었습니다.
```
```python
from random import *

date = randint(4, 28)
print("오프라인 스터디 모임 날짜는 매월 " + str(date) + "일로 선정되었습니다." )
# print("오프라인 스터디 모임 날짜는 매월",date,"일로 선정되었습니다." )
```



# reference
나도코딩 - 파이썬 코딩 무료 강의 (기본편)<br>
https://www.youtube.com/watch?v=kWiCuklohdY
