# 정렬
- Python, C++은 기본 정렬 메소드가 모두 stable sort를 지원한다.
- merge sort, bubble sort, insertion sort가 모두 stable sort이다.
- stable sort를 만들기 위해서 *decorate-sort-undecorate*패턴을 사용하기도 한다.
	- *순서를 나타내는 추가적인 키를 추가하여 sorting후에 original value를 순서대로 추출하는 패턴*

# 정규표현식
정규표현식 레퍼런스 및 학습 사이트
- https://regexr.com/
- https://regex101.com/
### 긍정형 전방탐색
- `(?=정규식)`를 사용해서 정규표현식을 매칭한후 정규식과 매칭된 해당 문자열을 소비하지 않고 다시 그 부분부터 매칭한다
### 부정형 전방탐색
- `(?!정규식)`를 사용해서 정규식과 매칭하지 않아야 매칭되고 해당 문자열을 소비하지 않는다.
### 그룹핑
- (?:)는 캡쳐하지 않는 그룹핑
- 
### 정규표현식을 통한 문자열 치환
```python
p = re.compile('[.]{2,}') # .이 2번 이상 연속된 문자열 매칭
s = p.sub('.', 'aa..bb...c')
# s = aa.bb.c
```
- `sub`메서드를 이용하여 첫번째 매개변수는 바꿀 문자열을 넣고 두번째 매개변수는 대상 문자열을 넣는다.
- 매칭하는 첫번째만 바꿀 경우는 `count=1`과 같이 추가 매개변수 `count`를 사용하여 바꿀 횟수를 지정할 수 있다.
### re 메소드
- `match`: 문자열 처음부터 매칭하는지
- `search`: 문자열 아무곳에서 매칭하는지
- `findall`: 매칭하는 모든것을 리스트로 리턴
- `split`: 해당 regex구분자를 통해 split한 문자열들을 리스트로 리턴
- `sub(패턴(regex), 대체할 문자열(repl), 대상 문자열(string))`: 문자열 치환
### 컴파일 옵션
```sql
p = re.compile('[a-z]', re.I)
```
- DOTALL or S: `.`이 줄바꿈 문자를 포함하여 모든 무자와 매치
- IGNORECASE or I: 대소문자 상관없이 매칭
- MULTILINE or M: `^`옵션을 각 라인과 매칭

### 문자클래스
- `\d`: 숫자와 매치
- `\D`: 숫자가 아닌 것과 매치
- `\s`: whitespace와 매치
- `\S`: whitespace가 아닌 것과 매치
- `\w`: 문자 혹은 숫자와 매치
- `\W`: 문자 혹은 숫자가 아닌 것과 매치

## 메타 문자
- `.`: newline `\n` 을 제외한 모든 문자와 매치
- `|`: or과 동일한 의미
- `^`: 문자열의 맨 처음과 일치
- `$`: 문자열의 끝과 매치
- `\b`: raw string과 같이 써야함, whitespace로 구분자, 매칭된 문자열에는 포함을 하지는 않음
- `\B`: whitespace로 구분된 단어가 아닌 경우만 매치

# 언어별 내장 함수, 클래스 정리 노트
## Python
- `map`은 lazy evaluation을 사용하므로 `list(map(람다, ...))` 과 같이 바로 리스트화 하지 않으면 안의 람다함수가 실행되지 않는다.
- 파이썬의 음수의 몫은 내림을 사용하고, 자바는 버림을 사용한다. 따라서 자바에서 왼쪽방향의 순환이동을 계산할때는 (나머지 결과 + 주기(원형큐사이즈))%주기(원형큐사이즈)로 계산한다.
### Python 비교 함수 사용
[파이썬 비교 함수](https://docs.python.org/ko/3/howto/sorting.html#comparison-functions) (`cmp_to_key`)는 Java의 Comparable을 implements하고 override하는 compare 메서드와 같은 용도로서 `key=` 형식으로 들어가는 인자에 함수(람다)로서 2개의 인자를 갖는 함수를 넣을 수 있으며 리턴값은 Java와 동일하게 작을땐 음수, 클땐 양수, 같을 땐 0을 리턴한다. **functools안에있는 모듈이므로 반드시 functools에서 import 해야한다.**
```python
from functools import cmp_to_key  
a = [5, 1, 3, 2]  
a.sort(key=cmp_to_key(lambda x, y: x - y))
### [1, 2, 3, 5]
```
### 문자열 패딩
`rjust`
- 오른쪽 정렬
- 전체 문자열 길이와 공백을 채울 문자 지정
```python
# 00077
val = '77'.rust(5, "0")
```
 `ljust`
- 왼쪽으로 정렬
- 전체 문자열 길이와 공백을 채울 문자 지정/
```python
# 00222
val = '222'.ljust(5, "0") 
```
 `zfill`
- 주어진 길이가 되도록 0을 왼쪽에 채워줌
```python
# 022
val = '22'.zfill(3)
```
`deque(maxlen=)`
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

# DFS
- BFS 사용한 모든 상태노드 탐색을 => DFS를 이용한 완전탐색으로 치환할 수 있다.
- DFS를 사용하여 고차원(다양한 제한 조건이 추가된)의 완전탐색을 하기 위해서는 다음과 같은 방법을 사용한다.
> 다음으로 방문할 수 있는 노드들의 집합은 반드시 deepcopy해주고 사용해야한다.
```python
def go(현재 노드를 가리키는 번호나 위치, 현재까지의 상태(visited배열), 현재 단계에서 나아갈 수 있는 다음 노드의 집합):
	다음 노드의 집합 deepcopy
	종료 조건 검사
	다음으로 방문할 수 있는 노드를 하나씩 방문
	 -> 이때 현재 단계에서 나아갈 수 있는 다음 노드의 집합에서 
	    선택한 노드를 제거하고 go()함수를 재귀호출한다.
	
```
> 방향의 우선순위가 정해지고 최단거리를 문제에서 정해주었을 땐 BFS보다 DFS가 `최적경로 찾기` 에 더 빠르고 쉽다 [예시 문제](https://school.programmers.co.kr/learn/courses/30/lessons/150365)

# 후위 표기식
## 중위 표기법을 후위 표기법으로 변환
  **1) 피연산자가 들어오면 바로 출력한다.**  
  **2) 연산자가 들어오면 자기보다 우선순위가 높거나 같은 것들을 빼고 자신을 스택에 담는다.**   
  **3) 여는 괄호 '('를 만나면 무조건 스택에 담는다.**   
  **4) 닫는 괄호 ')'를 만나면 '('를 만날 때까지 스택에서 출력한다.**   

## **후위 표기법 계산**
  **1) 피연산자를 만나면 스택에 담는다.**  
  **2) 연산자를 만나면 스택에서 두 개의 연산자를 꺼내서 연산한 뒤에 그 결과를 스택에 담는다.**   
  **3) 연산을 마치고 스택에 남아있는 하나의 피연산자가 연산 수행 결과이다.**  
  
# 언어별 유용한 테크닉
## Python
- 리스트의 최대 혹은 최소 값인 원소의 인덱스를 가져오기
```python
a = [1, 3, 2, 4]
max_index = max(range(배열 길이), key=lambda x: a[x])
```

# 누적합
## 구간의 변화 처리를 위한 누적합
### 1차원 배열
[1차원 배열 누적합을 이용한 카카오 문제 해설](https://tech.kakao.com/2021/01/25/2021-kakao-recruitment-round-1/#%EB%AC%B8%EC%A0%9C-5-%EA%B4%91%EA%B3%A0-%EC%82%BD%EC%9E%85) 

[1, 2, 3, 4, 5]의 배열이 있다고 가정했을 때 0번째부터 3번째 원소까지 각각 3만큼 빼야할때
[-3, 0, 0, 0, 3] 이라는 누적합 배열을 생성하여 누적합을 구해보면 [-3, -3, -3.  -3, 0]이 되어 원본 배열과 더했을 때 원하는 배열이 된다. 이러한 원리를 이용하여 일반화해보면  

> 1차원 배열에서 x번째 원소부터 y번째 원소까지 d만큼 변화를 주고 싶다면 원본배열의 길이 + 1 만큼의 새로운 배열을 선언하고 x번째 원소에 d만큼 더해주고 y + 1번째 원소에 d만큼 빼주면 된다. 

## 2차원 배열
[2차원 배열 누적합을 이용한 카카오 문제 해설](https://tech.kakao.com/2022/01/14/2022-kakao-recruitment-round-1/#%EB%AC%B8%EC%A0%9C-6-%ED%8C%8C%EA%B4%B4%EB%90%98%EC%A7%80-%EC%95%8A%EC%9D%80-%EA%B1%B4%EB%AC%BC)  

위의 1차원 배열의 아이디어를 2차원 배열로 확장하면 다음과 같다.  

![](images/Pasted%20image%2020230224181652.png) 

위의 배열을 왼쪽에서 오른쪽으로 위에서 아래로 누적합을 해주면 다음과 같이 된다.  

![](images/Pasted%20image%2020230224181402.png) 

>2차원 배열에서 (x1,y1)부터 (x2,y2)까지 n만큼의  변화는 (x1,y1)에 +n, (x. ,y2+1)에 -n, (x2+1,y1)에 -n, (x2+1,y2+1)에 +n을 한 것과 같습니다.

# 그래프
## 다익스트라
> 다익스트라를 조금 변형하면 시작점에서 다른 모든 정점까지 최단경로가 아닌 시작점에서 i지점까지 올 때 간선 가중치들의 최대값을  최소로하는 가중치를 구할 수 있다. [적용되는 문제 해설](https://tech.kakao.com/2022/07/13/2022-coding-test-summer-internship/#elementor-toc__heading-anchor-3)  
> 
> 다익스트라를 적용할 수 있는 이유는 경로가 지날 수록 단조 증가(같거나 커짐)하는 성질을 만족하기 때문이다.

```text
if dist[to] > dist[from] + weight then

dist[to] = dist[from] + weight

=> 다음과 같이 변형한다.

if intensity[to] > max(intensity[from], weight) then

intensity[to] = max(intensity[from], weight)
```
