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
