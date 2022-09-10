# 💡 B-Tree & B+Tree

## 1. B-Tree

![](https://velog.velcdn.com/images/wisdom-one/post/dc9a3b58-e987-4594-bc3f-598970ba6bf9/image.png)

이진 트리를 확장해서, 더 많은 수의 자식을 가질 수 있게 일반화시킨 균형 트리 (Balanced Tree) 자료구조의 일종이다.

`DB의 인덱스`는 B-tree 자료구조를 이용하여 테이블의 요소를 빠르게 탐색하도록 설계되어 있다.

<br/>

### 특징 및 규칙

최대 M개의 자식을 가질 수 있는 B트리를 `M차 B트리`라고 하며, 다음과 같은 특징을 가진다.
- 노드는 최대 M개 부터 M/2개 까지의 자식을 가질 수 있다.
- 노드에는 최대 M−1개 부터 [M/2]−1개의 키가 포함될 수 있다.
- 노드의 키가 x개라면 자식의 수는 x+1개다.
- 최소차수는 자식수의 하한값을 의미하며, 최소차수가 t라면 M=2t−1을 만족한다.
ex) 최소차수 t가 2라면 3차 B트리이며, key의 하한은 1개이다.

<br/>

규칙
- 노드의 자료 수가 N이면, 자식 수는 N+1이어야 한다.
- 각 노드의 자료는 정렬된 상태여야 한다.
- 루트 노드는 적어도 2개 이상의 자식을 가져야 한다.
- 루트 노드를 제외한 모든 노드는 적어도 M/2개의 자료를 가지고 있어야 한다.
- 단말 노드(leaf node)가 모두 같은 레벨에 있어야 한다.
- 입력 자료는 중복될 수 없다.

<br/>

## 2. B+Tree

![](https://velog.velcdn.com/images/wisdom-one/post/6f9dcbbb-8053-4807-affe-1373de09ed90/image.png)


B-Tree의 변형 구조로, **단말 노드(leaf node)가 연결리스트의 형태로 연결**되어 있어 선형 검색이 가능한 자료구조이다.

실제 DB의 인덱싱은 B+트리로 이루어져 있다고 한다. 이때 인덱스 부분의 key 값은 leaf에 있는 key 값을 직접 찾아가는데 사용한다.

<br/>

### B-Tree 와의 차이점
1. 모든 key, data가 단말 노드에 모여있다. B트리는 단말 노드가 아닌 각 key마다 data를 가진다면, B+트리는 단말 노드에 모든 data를 가진다.

2. 모든 단말 노드가 연결리스트의 형태를 띄고 있다. B트리는 옆에 있는 단말 노드를 검사할 때 다시 루트 노드부터 검사해야 한다면, B+트리는 단말 노드에서 선형검사를 수행할 수 있어 시간복잡도가 굉장히 줄어든다.

3. 단말 노드의 부모 key는 단말 노드의 첫번째 key보다 작거나 같다. 그림의 B+트리는 단말 노드의 key들을 트리가 가지고 있는 경우여서, data 삽입 또는 삭제가 일어날 때 트리의 key에 변경이 일어난다. 해당 경우뿐만 아니라 data의 삽입과 삭제가 일어날 때 트리의 key에 변경이 일어나지 않게 하여 더욱 편하게 B+트리를 구현하는 방법도 존재한다.

<br/>

### 특징
M차 B+트리는 다음과 같은 특징을 가진다.
- 노드는 최대 M개 부터 M/2개 까지의 자식을 가질 수 있다.
- 노드에는 최대 M−1개 부터 [M/2]−1개의 키가 포함될 수 있다.
- 노드의 키가 x개라면 자식의 수는 x+1개 이다.
- 최소차수는 자식수의 하한값을 의미하며, 최소차수가 t라면 M=2t−1을 만족한다. 
ex) 최소차수 t가 2라면 3차 B트리이며, key의 하한은 1개다.

<br/>

## 3. DB 인덱스로 B-Tree 계열을 사용하는 이유

DB 인덱스로 B-Tree가 적합한 이유는 아래 세 가지다.
실제로 가장 유명한 DBMS 중 하나인 Oracle도 B-Tree를 주로 이용한다.

1. 트리 내 모든 데이터가 항상 정렬된 상태로 유지되기 때문에, 등호(=) 연산뿐만 아니라 부등호(>, <) 연산 처리도 가능하다.
2. 포인터 접근 방식이 적어 매우 많은 데이터가 있어도 속도 이슈가 적다.
3. 데이터 탐색뿐 아니라, 삽입 및 수정 및 삭제에도 항상 O(log N)의 시간 복잡도를 가진다.

<br/><br/>

## 🔖 참고
- [B-Tree & B+Tree](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Data%20Structure/B%20Tree%20%26%20B%2B%20Tree.md)
- [[자료구조] 그림으로 알아보는 B-Tree
](https://velog.io/@emplam27/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-B-Tree)
- [[자료구조] 그림으로 알아보는 B+Tree](https://velog.io/@emplam27/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-B-Plus-Tree)
- [B-Tree 계열을 쓰는 이유](https://siahn95.tistory.com/entry/DB-%EC%9D%B8%EB%8D%B1%EC%8A%A4%EB%9E%80-2-%EA%B5%AC%EC%A1%B0-B-Tree-%EA%B3%84%EC%97%B4%EC%9D%84-%EC%93%B0%EB%8A%94-%EC%9D%B4%EC%9C%A0)
