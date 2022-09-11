# B-Tree & B+Tree

## A. (시작하기 전) 이진 트리

- 이진 트리: 각각의 노드가 최대 두 개의 자식 노드를 가지는 트리 자료구조

- Full Binary Tree(정 이진 트리): 모든 노드가 0개 또는 2개의 자식 노드만 갖는 트리
- Complete Binary Tree(완전 이진 트리): 위에서 아래로, 왼쪽에서 오른쪽으로 순서대로 차곡차곡 채워진 이진 트리
- Perfect Binary Tree(포화 이진 트리): 모든 내부 노드가 2개의 자식 노드를 가지고 모든 리프 노드가 동일한 레벨(혹은 깊이)를 가지는 것

- Balanced Binary Tree(균형 이진 트리): 오른쪽 서브트리의 높이와 왼쪽 서브트리의 높이 차이가 1 이하인 이진 트리

B-Tree, B+Tree는 균형이진탐색트리의 일종

<img src="https://adrianmejia.com/images/full-complete-perfect-binary-tree.jpg">

<br>

## B. B-Tree

> 이진 트리를 확장해 하나의 노드가 가질 수 있는 자식 노드의 최대 숫자가 2보다 큰 트리 구조

<br>

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20200506235136/output253.png">

<br>

### B-Tree의 특징

- 각 노드의 자료는 정렬되어 있다.
- 자료는 중복되지 않습니다.
- 모든 leaf node는 같은 레벨에 있다.
- root node는 자신이 leaf node가 되지 않는 이상 적어도 2개 이상의 자식을 가진다.
- root node가 아닌 노드들은 적어도 M/2개의 자식 노드를 가지고 있다. (최대 M개)

<br>

### B-Tree의 시간복잡도

| Sr. No. | Algorithm | Time Complexity |
| ------- | --------- | --------------- |
| 1.      | Search    | `O(log n)`      |
| 2.      | Insert    | `O(log n)`      |
| 3.      | Delete    | `O(log n)`      |

<br>

## C. B+Tree

<br>

- B+Tree는 오직 leaf node에만 데이터를 저장하고 leaf node가 아닌 node에서는 자식 포인터만 저장한다.
- leaf node끼리는 Linked list로 연결되어 있다.
- 반드시 leaf node에만 데이터가 저장되기 때문에 중간 node에서 key를 올바르게 찾아가기 위해서 key가 중복될 수 있다.

<br>

### B+Tree의 장단점

장점

- leaf node를 제외하고 데이터를 저장하지 않기 때문에 메모리를 더 확보할 수 있다.
  - 하나의 node에 더 많은 포인터를 가질 수 있기 때문에 트리의 높이가 더 낮아지므로 검색 속도를 높일 수 있다.
- Full scan 시 leaf node에만 데이터가 저장되어 있고, leaf node끼리 linked list로 연결되어 있기 때문에 선형 시간이 소모된다.

<br>

단점

- 반드시 특정 key에 접근하기 위해서 leaf node까지 가야 한다.

<br>

### B-Tree와 B+Tree의 차이

<br>

- B-Tree

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FSvp6z%2FbtrdEi9c2DR%2FR4Dnmqkl8RWcqQPBACI9fK%2Fimg.png">

<br>

- B+Tree

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbAARBC%2FbtrdDydoUp7%2F9h4KOXBRyDNKpKDAe2ugq0%2Fimg.png">

<br>

## C. 참고자료

🔗 출처 : https://ssocoit.tistory.com/217 [코딩하는 경제학도]

🔗 출처: https://rebro.kr/167?category=484170 [Rebro의 코딩 일기장:티스토리]
