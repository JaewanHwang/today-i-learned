
## 문자열 패딩
### `rjust`
- 오른쪽 정렬
- 전체 문자열 길이와 공백을 채울 문자 지정
```python
# 00077
val = '77'.rust(5, "0")
```
### `ljust`
- 왼쪽으로 정렬
- 전체 문자열 길이와 공백을 채울 문자 지정/
```python
# 00222
val = '222'.ljust(5, "0") 
```
### `zfill`
- 주어진 길이가 되도록 0을 왼쪽에 채워줌
```python
# 022
val = '2'.zfill(3)
```
### `deque(maxlen=)`
- maxlen 파라미터는 덱의 최대크기를 지정하며 최대 크기에서 새로운 원소를 append 할 시 가장 오래된 항목(head에 가까운 노드)부터 제거한다
```python
q = deque(maxlen=3)
q.append(1)
q.append(2)
q.append(3)
q.append(4)
# deque([2, 3, 4])
q.appendleft(5)
# deque([5, 2, 3])
```