# 1. B-Tree

![image](https://user-images.githubusercontent.com/100047095/189522179-17649c39-da4b-4fb8-8f9b-2284046ca7e1.png)
출처 : [https://ssup2.github.io/theory_analysis/B_Tree_B+_Tree/](https://ssup2.github.io/theory_analysis/B_Tree_B+_Tree/)

<br/>

- Binary Search Tree를 확장한 Tree로 각 노드는 여러개의 키를 가질 수 있고 여러개의 child를 가질 수 있음
- 모든 Leaf Node는 동일한 Depth를 가짐
- N Order B-Tree의 각 Node는 N-1개의 Key를 가질 수 있고 최대 N개의 Child를 가질 수 있음
    - 위의 사진은 3 Order B-Tree이므로 최대 2개의 key를 가질 수 있고 최대 3개의 Child를 가질 수 있음
- 각 노드는 여러개의 key를 가지고 있고 각 key에 대응되는 Data도 같이 가짐
- 새로운 키 값은 leaf 노드에 삽입 됨
- node 내의 키 값들은 모두 오름차순임


<br/><br/>

# 2. B+Tree

- B-Tree의 변형 구조로 index 부분과 leaf 노드로 구성된 순차 data 부분으로 이루어짐
- B-Tree에서는 특정 key 값이 하나의 노드에서만 존재할 수 있지만 B+ 트리에서는 leaf 노드와 leaf의 부모 노드에서 공존할 수 있음 → B+Tree의 leaf가 아닌 노드들은 데이터의 빠른 접근을 위한 인덱스 역할만 하기 때문임


<br/><br/>

# 3. B-Tree vs B+Tree

**공통점**

1. 모든 leaf의 depth가 같음
2. 각 node에는 k/2 ~ k개의 item이 들어있어야 함
3. 삽입 시 오버플로우가 발생하면 split함
4. 삭제 시 언더플로우가 발생하면 redistribution하거나 merge함

**차이점**

1. B-Tree의 각 노드에서는 key 뿐 아니라 data도 들어갈 수 있음 반면 B+Tree에서는 각 노드에는 key만 들어가야 함 data는 leaf에만 존재
2. B+Tree는 B-Tree와 달리 add, delete가 leaf에서만 일어남
3. B+Tree는 leaf node끼리 linked list로 연결되어 있음
