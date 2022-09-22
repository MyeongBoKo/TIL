# ■ 집합 메서드
## 1. add
이미 만든 set 자료형에 값을 추가
한 개의 값을 추가할 때 사용  
여러값을 추가하려고 하면 에러 발생
```python
s1 = set([3, 6, 9])
s1.add(12)
s1
# {9, 3, 12, 6}

s1.add(15, 18)
# Traceback (most recent call last): File "<pyshell#17>", line 1, in <module> s1.add(15, 18) TypeError: set.add() takes exactly one argument (2 given)
```

## 2. update
여러 값을 추가할 때 사용
```python
s1 = set([3, 6, 9])
s1.update([2, 4, 8])
s1
# {2, 3, 4, 6, 8, 9}
```

## 3. remove
특정 값 제거시 사용
```python
s1 = {2, 3, 4, 6, 8, 9}
s1.remove(3)
s1
# {2, 4, 6, 8, 9}
```

# reference
점프 투 파이썬 - 박응용<br>
https://wikidocs.net/
