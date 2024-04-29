## BFS, DFS

### 너비 우선 탐색 (BFS)

그래프 탐색 알고리즘으로 **같은 깊이에 해당하는 정점**부터 탐색하는 알고리즘

- **Queue를 이용하여 구현할 수 있다.**

- 시작 지점에서 가까운 정점부터 탐색한다.

- V가 정점의 수, E가 간선의 수 일때 BFS의 시간 복잡도는 O(V+E)(빅오 v+e)다.

<br />

---

<img width="675" alt="스크린샷 2024-04-26 201634" src="https://github.com/yookeunbyul/cs-study/assets/91243651/dc435239-a168-46b5-8545-db5cf7dd32a9">

1. A를 시작지점이라고 생각하고 A를 enQueue해준다.

2. 그리고 A를 deQueue 해주고 A에서 갈 수 있는 정점인 B,C,D를 enQueue 해준다.

3. B를 deQueue 해주고 B에서 갈 수 있는 정점인 F를 enQueue 해준다. C는 이미 enQueue 되어있기 때문에 패스한다.

4. C를 deQueue 해주고 F는 이미 enQueue 되어있기 때문에 패스한다.

5. D를 deQueue 해주고 D에서 갈 수 있는 E를 enQueue 해준다.

6. F를 deQueue 해주고 F에서 갈 수 있는 G를 enQueue 해준다.

7. E를 deQueue 해주고 E에선 갈 수 있는 정점이 없으니 패스한다.

8. G를 deQueue 해주고 G에선 갈 수 있는 정점이 없으니 그대로 종료된다.

<br />

---

### 깊이 우선 탐색 (DFS)

그래프 탐색 알고리즘으로 **최대한 깊은 정점부터 탐색**하는 알고리즘

- **Stack을 이용하여 구현할 수 있다.**

- 시작 정점에서 깊은 것 부터 찾는다.

- V가 정점의 수, E가 간선의 수 일때 BFS의 시간 복잡도는 O(V+E)(빅오 v+e)다.

<br />

---

<img width="698" alt="스크린샷 2024-04-26 203759" src="https://github.com/yookeunbyul/cs-study/assets/91243651/fd684ff3-5c21-487c-9dde-ef7ee2c9c8b3">

1. A부터 시작해서 stack에 push 해준다.

2. A에서 갈 수 있는 정점인 B를 push 해준다.

3. B에서 갈 수 있는 정점인 F를 push 해준다.

4. F에서 갈 수 있는 정점인 C를 push 해준다.

5. C에서 갈 수 있는 정점이 없기 때문에 C를 pop해주고 F에서 갈 수 있는 G를 push 해준다.

6. G에서 갈 수 있는 정점이 없기 때문에 G,F,B를 pop해준다.

7. A에서 갈 수 있는 정점인 D를 push 해준다.

8. D에서 갈 수 있는 정점인 E를 push 해준다.

9. 더이상 갈 수 있는 정점이 없으니 모두 pop 해주고 탐색을 종료한다.
