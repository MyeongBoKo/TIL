# 클래스
- `클래스`란 똑같은 무언가를 계속해서 만들어낼 수 있는 설게 도면(뽑기, 틀)
- `인스턴스`란 클래스에 의해서 만들어진 피조물(별 또는 하트가 찍힌 뽑기)
```python
class Simple:
    pass

// 위의 클래스는 아무런 기능도 갖고 있지 않은 껍질뿐인 클래스.
// 이런 클래스도 인스턴스라는 것을 생성하는 기능을 가지고 있다.
```
```python
# Simple이라는 클래스의 인스턴스를 만드는 방법
a = Simple()    // Simple()의 결과값을 돌려받는 a가 인스턴스


// 인스턴스는 클래스에 의해서 만들어진 객체, 1개의 클래스에서 무수히 많은 인스턴스를 만들 수 있다.
```
## 예제
```python
class Service:
    secret = "영구는 배꼽이 두 개다"
    def setname(self, name):
        self.name = name
    def sum(self, a, b):
        result = a + b
        print("%s님 %s + %s = %s입니다." %(self.name, a, b, result))

# class 이용하는 방법
iu = Service()
iu.secret
'영구는 배꼽이 두 개다'

iu.setname("ii")    // iu와 ii라는 이름을 연결해 주는 것이 self이다.

iu.sum(1, 2)
ii님 1 + 2 = 3입니다.
```
### self란
- `self`는 클래스 안에 있는 함수를 접근할 때 인스턴스가 제대로 생성되었는지 확인한다.
- `iu.sum(iu, 1, 2)` 이때 self는 호출 시 이용했던 인스턴스로 바뀐다. 그래서 `iu.sum(1, 2)`로 사용가능하다.
- 파이썬에서는 클래스 내 함수의 첫 번째 인수는 무조건 self로 사용해야 인스턴스 함수로 사용할 수 있다.

#### iu.setname("ii") 순서
1. `iu.setname("ii")`
2. self.name = name
3. iu.name = name       // self는 첫 번째 입력값으로 iu라는 값을 가지고 온다.
4. iu.name = "ii"
- self.name이 iu.name로 치환 

```python
class Service:
    secret = "영구는 배꼽이 두 개다"
    def __init__(self, name):
        self.name = name
    def sum(self, a, b):
        result = a + b
        print("%s님 %s + %s = %s입니다." %(self.name, a, b, result))

        
iu = Service("ii")
iu.sum(1,2)
ii님 1 + 2 = 3입니다.
```
#### __init__
- __init__란 인스턴스를 만들 때 항상 실행한다는 의미를 가지고 있다.

#### type()
- 파이썬 자체적으로 가지고 있는 내장 함수로 객체의 타입을 출력
- 인스턴스를 생성하는 동시에 초깃값을 준다.

## 클래스의 상속
`class 상속받을 클래스명(상속할 클래스명)`

# 모듈
- 함수나 변수 또는 클래스들을 모아 놓은 파일
- 다른 파이썬 프로그램에서 불러와 사용할 수 있게끔 만들어진 파이썬 파일
## 도스 창에서 가져오는 방법
1. `window + r` > `cmd` 입력
2. `cd C:\내가 불러오고 싶은 파일의 위치`
3. `C:\내가 불러오고 싶은 파일의 위치>dir`
4. `C:\내가 불러오고 싶은 파일의 위치>python`
5. import `파일 이름`
6. 수행할 문장(파일이름.함수)

- 이때 import는 이미 만들어진 파이썬 모듈을 사용할 수 있게 해주는 명령어
- 모듈이용하는 방법    
    `import 모듈이름`
   ```python
    import mod1
    print(mod1.sum(3, 4))
   ```

- 다른 방법
   - `from 모듈이름 import 모듈함수`
    ```python
    from mod1 import sum
    sum(3, 4)
    7
    ```

- `if__name__ == "__main__":`
  - __name__ == "__main__":이 참이 되어 if 문 다음 문장 실행
  - 거짓이면 if 문 실행 x

- 모듈에 포함된 변수, 클래스, 함수 찾기
`모듈이름.함수() or 변수 등등)`

# 패키지
- `__inti__.py` : 해당 디렉터리가 패키지 일부임을 알려주는 역할을 한다.

# 예외 처리

### 1. try - except
- try - except는 오류 처리를 위해 사용
- try 블럭 수행 중 오류가 발생하면 except 블럭이 수행
- try 블럭에서 오류가 발생하지 않으면 except블럭은 수행X
```python
try:
    ...
except[발생 오류[as 오류 메세지 변수]]:
    ...
```
- `except[발생 오류[as 오류 메세지 변수]]:`에서 [] 기호를 사용하는데, 괄호를 생략할 수 있고, 3가지로 표현한다.
1. ```python
   # 오류 종류에 상관없이 오류가 발생하기만 하면 except 블록을 수행
   try:
        ...
    except:
        ...
   ```

2. ```python
   # 오류가 발생하면 except 문에 미리 정해 놓은 오류 이름과 일치할 때만 except 블록을 수행
   try:
        ...
    except 발생 오류:
        ...
   ```

3.  
   ```python
   # 두 번째 경우에서 오류 메세지의 내용까지 알고 싶을 때 사용
   try:
        ...
    except 발생 오류 as 오류 메세지 변수:
        ...
   ```

### 2. try - else
- try문은 else절을 지원
- else절은 예외가 발생하지 않는 경우에 실행되며 반드시 except절 바로 다음에 위치
```python
try:
    f = open('foo.txt', 'r')
except FileNotFoundError as e:
    print(str(e))
else:
    data = f.read()
    f.close()

# foo.txt라는 파일이 없으면 except절이 수행. foo.txt파일이 있으면 else절이 수행
```
### 3. try finally
- try문에서 finally절을 사용하는데, finally절은 try문 수행 도중 예외 발생 여부에 상관없이 항상 수행
- finally절은 사용한 리소를 close해야 할 경우에 많이 사용
```python
f = open('foo.txt', 'r')
try:
    # 무엇가를 수행
finally:
    f.close()
```

4. 오류 회피하기
- pass를 이용해서 오류를 그냥 회피한다.
```python
try:
    f = open("나없는 파일", 'r')
except FileNotFoundError:
    pass
```

5. 오류를 일부러 발생
- 프로그램을 실행시키기 위해 일부러 오류를 발생시킨다.
```python
class Bird:
    def fly(self):
        raise NotImplementedError   
        # 파이썬 내장 오류로 꼭 자겅해야 하는 부분이 구현되지 않았을 경우에 일부러 오류를 발생시킴
```
```python
class Eagle(Bird):
    pass

eagle = Eagle()
eagle.fly()
# 오류가 발생
```
```python
class Eagle(Bird):
    def fly(self):
        print("very fast")

eagle = Eagle()
eagle.fly()

# very fast
```

# reference
점프 투 파이썬 - 박응용
