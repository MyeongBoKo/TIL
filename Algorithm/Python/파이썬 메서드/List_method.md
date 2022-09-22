# ■ 리스트 메서드
## 1. append
append(x) 리스트의 맨 마지막에 x를 추가하는 함수  
x는 어떤 자료형도 추가 가능.
```python
a = [1, 2, 3]
a.append(4)
a
# [1, 2, 3, 4]

a.append([5,6])
a
# [1, 2, 3, 4, [5, 6]]

a.append('apple')
a
# [1, 2, 3, 4, [5, 6], 'apple']
```

## 2. extend
extend(literable) 메서드는 literable 자료형만 올 수 있다.
```python
a = [1, 2, 3]
a.extend([4, 5])
a
# [1, 2, 3, 4, 5]

a.extend(6)
# Traceback (most recent call last): File "<pyshell#29>", line 1, in <module> a.extend(6) TypeError: 'int' object is not iterable
b = [7, 8]

a.extend(b)
a
# [1, 2, 3, 4, 5, 7, 8]
```

## 3. insert
insert(i, x) 함수는 i번째 위치에 x를 삽입하는 함수이다.   
이때 i의 값에 음수를 넣으면 배열의 끝을 기준으로 한다.   
```python
a = [3, 6, 9]
a.insert(1, 2)
a
# [3, 2, 6, 9]

a = ['h', 'p', 'p', 'y']
a.insert(2, 1)
a
# ['h', 'p', 1, 'p', 'y']
a.insert(2, '1')
a
# ['h', 'p', '1', 1, 'p', 'y']

a.insert(-1, 9)
a
# ['h', 'p', '1', 1, 'p', 9, 'y']
```

## 4. sort
리스트 요소를 순서대로 정렬
```python
a = [3, 1, 2, 9, 8]
a.sort()
a
# [1, 2, 3, 8, 9]

b = ['b','a','f','e','g', 'c']
b.sort()
b
# ['a', 'b', 'c', 'e', 'f', 'g']
```

## 5. reverse
현재의 리스트를 거꾸로 정렬
```python
a = ['d', 'a', 'f']
a.reverse()
a
['f', 'a', 'd']
```

## 6. index
index(x) 리스트에 x 값이 있으면 x의 위치를 반환.     
이때 중복된 값이 있으면 앞에 있는 값으로 위치를 반환
```python
a = [1, 2, 3, 9, 8, 9]
a.index(2)
# 1

a.index(7)
#Traceback (most recent call last): File "<pyshell#55>", line 1, in <module> a.index(7) ValueError: 7 is not in list

a.index(9)
# 3
```
## 7. remove
```python
a = [1, 2, 3, 9, 8, 9]
a.remove(9)
a
[1, 2, 3, 8, 9]
```

## 8. pop
리스트의 맨 마지막에 있는 요소를 돌려주고, 그 요소를 삭제
```python
a = [1, 2, 3, 8, 9]
a.pop()
# 9

a
# [1, 2, 3, 8]

a.pop(2)    # index가 2인 위치의 요소를 돌려주고, 그 요소 삭제
3
a
# [1, 2, 8]
```

## 9. count
```python
a = [1, 2, 3, 9, 8, 9]
a.count(9)
# 2
```

# reference

점프 투 파이썬 - 박응용<br>
https://wikidocs.net/
append(), extend(), insert() 비교<br>
https://ooyoung.tistory.com/117
