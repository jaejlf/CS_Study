# 트라이(Trie)

<br>

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/b/be/Trie_example.svg/800px-Trie_example.svg.png">

<br>

> 문자열을 저장하고 효율적으로 탐색하기 위한 트리 형태의 자료 구조

<br>

일반적인 이진 트리 검색 시 `O(M*logN)`의 시간이 걸리지만(`M`: 문자열 최대 길이, `N`: 트리의 키 개수) 트라이를 사용하면 `O(M)` 시간만에 탐색이 가능하다.

<br>

## A. 사용 목적

- 문자열 탐색
  - 장점: 빠르게 탐색이 가능하다
  - 단점: 각 노드에서 자식들에 대한 포인터들을 배열로 모두 저장하고 있다는 점에서 저장 공간의 크기가 크다
  - ex) 검색어 자동완성, 사전 검색, 문자열 검사
- 시간복잡도
  - 제일 긴 문자열의 길이: `L`, 총 문자열들의 수: `M` 일 때의 시간복잡도
    - 생성: `O(M*L)`
    - 탐색: `O(L)`

<br>

## B. 연산

<br>

### 📌 구조

```
 structure Node
   Children Node[Alphabet-Size]
   Is-Terminal Boolean
   Value Data-Type
 end structure
```

<br>

### 검색

```
 Trie-Find(x, key)
   for 0 ≤ i < key.length do
     if x.Children[key[i]] = nil then
       return false
     end if
     x := x.Children[key[i]]
   repeat
   return x.Value
```

<br>

#### 검색 예시

<br>

<img src="https://velog.velcdn.com/images%2Fkimdukbae%2Fpost%2Fbc255f08-81f6-4031-8ac6-ca8f465ca7a3%2Fimage.png">

<br>

Q1. `트라이`에 'abc' 문자열이 있는지 탐색

- Head의 child에 'a'가 존재 → 'a' 노드(key='a')로 이동
- 'a' 노드의 child에 'b'가 존재 → 'b' 노드(key='b')로 이동
- 'b' 노드의 child에 'c'가 존재 → 'c' 노드(key='c')로 이동
- 문자열 탐색이 완료됨 → 현재 노드 ('c'노드)에서 Data값이 존재 → 따라서 'abc' 문자열이 존재함을 알 수 있음

<br>

Q2. 'ca'라는 문자열이 있는지 탐색

- Head의 child에 'c'가 존재 → 'c' 노드(key='c')로 이동
- 'c' 노드의 child에 'a'가 존재 → 'a' 노드(key='a')로 이동
- 문자열 탐색이 완료됨 → 현재 노드 ('a'노드)에서 Data값이 없음 → 따라서 'ca' 문자열은 존재 X
