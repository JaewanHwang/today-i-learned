
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
## 정렬
- Python, C++은 기본 정렬 메소드가 모두 stable sort를 지원한다.
- merge sort, bubble sort, insertion sort가 모두 stable sort이다.
- stable sort를 만들기 위해서 *decorate-sort-undecorate*패턴을 사용하기도 한다.
	- *순서를 나타내는 추가적인 키를 추가하여 sorting후에 original value를 순서대로 추출하는 패턴*

## 정규표현식

### 긍정형 전방탐색
- `(?=정규식)`를 사용해서 정규표현식을 매칭한후 정규식과 매칭된 해당 문자열을 소비하지 않고 다시 그 부분부터 매칭한다
### 부정형 전방탐색
- `(?=정규식))`를 사용해서 정규식과 매칭하지 않아야 매칭되고 해당 문자열을 소비하지 않는다.