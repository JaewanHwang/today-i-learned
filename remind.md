# [여행경로](https://school.programmers.co.kr/learn/courses/30/lessons/43164)
\#DFS \#모든 엣지 탐색
- 모든 엣지를 탐색하는 DFS를 수행하는 문제
- 문제에서는 사전순으로 가장 빠른 경로를 출력
- 따라서 연결 리스트의 모든 노드마다 오름차순 정렬 후 먼저 정답이 출력되는 것이 정답
- DFS를 통한 완전탐색은 복원이 중요한데 모든 엣지를 탐색해야 하므로 연결리스트에 대해 `pop(i)`, `go(...)`, `insert(i, ...)`를 사용할 수 있다.(visited로 처리해도 됨)
# [호텔 방 배정](https://school.programmers.co.kr/learn/courses/30/lessons/64063)
\#Union-Find \#Prim \#Path Compression \#Linked List
- 시간복잡도를 줄이기 위해 Union-Find 알고리즘에서 쓰이는 Path Compression을 사용하면 효율성 테스트를 통과함
- Path Compression의 시간복잡도는 O(logN)이므로 최종적으로 O(NlogN)이 되어 3,600,00정도의 연산이 필요
- Path Compression에서 return값은 다음과 같이 다음 노드(현재노드 + 1)를 반환
```python
def go(num, room_dict):
    if num not in room_dict:
        room_dict[num] = num + 1
        return room_dict[num]
    room_dict[num] = go(room_dict[num], room_dict)
    return room_dict[num]
```
# [파괴되지 않은 건물](https://school.programmers.co.kr/learn/courses/30/lessons/92344)
\#누적합 \#2차원 배열 누적합 \#2차원 배열 구간의 변화
- 애초에 시뮬레이션을 하면 O(N * M * K)라는 시간복잡도로 인해 효율성 테스트를 통과하지 못함
- 따라서 누적합을 이용해서 O(1)만에 skill을 처리해야함
- 이때 이차원 배열의 직사각형 범위 전체를 어떤 값을 더하거나 빼기 위해서는 누적합 배열을 따로 생성해야함
- 누적합 배열은 (N + 1) * (M + 1) 크기로 만들어야함
- 누적합 배열은 아래와 같이 (x1,y1)에 +n, (x1,y2+1)에 -n, (x2+1,y1)에 -n, (x2+1,y2+1)에 +n을 해줌
	 ![](images/Pasted%20image%2020230224175744.png)
- 모든 skill에 대해 누적합 배열을 처리하면 왼쪽에서 오른쪽으로 누적합을 해주고 위에서 아래쪽으로 누적합을 해주면 누적합 배열을 완성할 수 있음
- 최종적으로 누적합 배열 + board 배열을 해주면 모든 skill이 끝난뒤 board 배열을 얻을 수 있게 됨
# [코딩 테스트 공부](https://school.programmers.co.kr/learn/courses/30/lessons/118668)
\#unbounded knapsack \#dp \#dynamic programming \#동적 계획법
- 처음에 문제를 풀때는 0-1냅색을 변형하여 풀었지만 실패가 계속 떴음
- 목표로 하는 목표 알고력과 목표 코딩력을 넘어가는 경우까지 고려하면 배열의 크기 및 업데이트 횟수가 상당히 많아 지므로 시간 초과가 나게됨
- 이를 해결하기 위해 목표 알고력, 코딩력을 넘어가면 목표 알고력과 목표 코딩력으로 세팅해주면 된다.
- 또한 최대 alp_req나 최대 cop_req가 오히려 초기 알고력과 코딩력보다 작을 수 있으므로 둘 중 큰 값으로 최대 목표치들을 세팅해줘야한다.
- 보통의 0-1 Knapsack 알고리즘은 하나의 아이템마다 무게별로 dp배열을 업데이트한다.
- 이는 딱 하나만 사용하면 되기 때문에 사용하는 loop 순서로 만약 bounded knapsack이나 unbounded knapsack의 경우 아래과 같이 0-1 knapsack처럼 loop를 돌게 되면 최적값을 찾는다고 보장할 수 없다.
```text
for item in items:
	for w in W:
		d[w] = max(d[w], d[w - item's w] + items's benefit
```
- 따라서 만약 dp문제인데 냅색의 느낌이 난다면 0-1 Knapsack이 아니라면 다음과 같이 일반적이 bottom-up 방식의 dp처럼 풀면 최적값을 보장할 수 있다.
```text
for w in W:
	for item in items:
		d[w + item's weight] = max(d[w + item's weight], d[w] + items's benefit)
```
# [사라지는 발판](https://school.programmers.co.kr/learn/courses/30/lessons/92345)
\#게임 이론, \#턴 게임
[카카오 해설](https://tech.kakao.com/2022/01/14/2022-kakao-recruitment-round-1/#%EB%AC%B8%EC%A0%9C-7-%EC%82%AC%EB%9D%BC%EC%A7%80%EB%8A%94-%EB%B0%9C%ED%8C%90)
- 완전탐색으로 A함수, B함수를 각각 만들어 리턴값은 승패여부와 이동 횟수를 넘긴다.
- 각각의 함수에서 상대방 함수를 호출하므로 상대방 함수의 결과에 따라 나의 결과가 정해진다.
- 이때 게임 이론에 따라 실수 없이 최적의 플레이한 결과를 얻기 위해선 상대방이 모두 이기는 경우에만 내가 지는 걸로 하고 상대방이 한번이라도 질 수 있는 경우면 내가 이기는 걸로 리턴해야 최적의 플레이와 동시에 질 수 밖에 없는 상황을 만들 수 있다.