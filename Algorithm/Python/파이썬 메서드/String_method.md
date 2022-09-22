# ■ 문자열 메서드
## 1. count - 문자 개수 세기
```python
a = "apple"
a.count('p')
# 2 (int)
```

## 2. find  - 위치 알려주기1
```python
a = "Just do it"
a.find('t')
# 3 (int)
a.find('a')
# -1 (int)  - 내가 찾고자 하는 문자 또는 문자열이 존재하지 않는 경우 -1을 반환

```

## 3. index - 위치 알려주기2
```python
a = "Believe in yourself"
a.index('i')
# 3 (int)- 중복되는 문자가 존재할 경우 맨 앞에 있는 문자 또는 문자열의 위치를 반환
a.index('a')
# 오류 발생
```

## 4. join - 문자열 삽입
문자열 각각의 문자 사이에 사용자가 입력한 값을 삽입
```python
a = "Just do it"
':'.join(a)
# 'J:u:s:t: :d:o: :i:t' (str)

','.join("happy")
# 'h,a,p,p,y' (str)

```

## 5. upper - 소문자를 대문자로 바꾸기
```python
a = "Belive in yourself"
a.upper()
# 'BELIVE IN YOURSELF' (str)
```

## 6. lower - 대문자를 소문자로 바꾸기
```python
a  = 'BELIVE IN YOURSELF'
a.lower()
# 'belive in yourself' (str)
```

## 7.  lstrip - 왼쪽 공백을 지우기
```python
a = " dog "
a.lstrip()
# 'dog ' (str)

```

## 8.  rstrip - 오른쪽 공백을 지우기
```python
a = ' dog '
a.rstrip()
# ' dog' (str)
```
## 9. strip - 양쪽 공백 지우기
```python
a = ' dog '
a.strip()
# 'dog' (str)
```

## 9.  replace - 문자열 바꾸기
replace(바뀌게 될 문자열, 바꿀 문자열)
```python
a = 'I am angry'
a.replace('angry', 'happy')
# 'I am happy' (str)
```

## 10. split - 문자열 나누기
```python
a = "Just do it"
a.split()
# ['Just', 'do', 'it'] (str)

a = '1:2:3:4'
a.split(':')
# ['1', '2', '3', '4'] (str)

a.split(:)
# SyntaxError: invalid syntax 
```
# reference
점프 투 파이썬 - 박응용<br>
https://wikidocs.net/
