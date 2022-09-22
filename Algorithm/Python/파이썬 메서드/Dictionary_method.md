#  ■ 딕셔너리 메서드
## 1. keys - Key 리스트 만들기
딕셔너리 a의 key만을 모아서 dic_keys 객체를 돌려줌.   
리스트가 아니기 때문에 리스트 내장 함수는 사용불가.
반환 값으로 리스타가 필요한 경우에 list(a.keys())를 사용.
```python
a = {'A': '1', 'B': '2', 'C': '3'}
a.keys()
# dict_keys(['A', 'B', 'C'])

list(a.keys())
# ['A', 'B', 'C']
```

## 2. values - Value 리스트 만들기
```python
a.values()
# dict_values(['1', '2', '3'])

list(a.values())
# ['1', '2', '3']
```


## 3. items - Key, Value 쌍 얻기
Key와 Value의 쌍을 튜플로 묶은 값을 dic_items 객체로 돌려줌.
리스트를 사용하는 것과 동일하게 사용
```python
a.items()
# dict_items([('A', '1'), ('B', '2'), ('C', '3')])
```


## 4. clear - Key:Value 쌍 모두 지우기
```python
a.clear()
a
# {}
```


## 5. get - Key로 Value 얻기
get(x) 함수는 x라는 Key에 대응되는 Value를 돌려줌.   
`a.get('A')`의 `결과값`하고, `a['A']`의 `결과값`은 같음.   
딕셔너리 안에 존재하지 않는 키를 가져오려고 할 경우에는 에러를 발생시킴   
`get(x, '디폴트')`의 경우 존재하지 않는 키를 사용하면 디폴트 값을 가져옴.
```python
a = {'A': '1', 'B': '2', 'C': '3'}
a.get('A')
# '1'
a.get('B')
# '2'
```


## 6. in - 해당 Key가 딕셔너리 안에 있는지 조사
`boolean`으로 반환값을 출력
```python
'A' in a
# True
'a' in a
#False
```


# reference
점프 투 파이썬 - 박응용<br>
https://wikidocs.net/
