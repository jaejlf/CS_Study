> 최소 공통 조상은 트리 구조에서 임의의 두 node가 갖는 가장 가까운 조상 node를 의미함. 아래 그림에서 4번 정점과 3번 정점의 LCA는 1번 정점임.
> 

<br/>

![image](https://user-images.githubusercontent.com/100047095/198876431-164a5920-f3ec-49f7-a6e8-cc697fb3d4b9.png)

<br/><br/>

## 1. 선형 탐색

가장 단순한 방법으로 두 포인터를 두고 가리키는 정점이 같을 때까지 부모 노드로 거슬러 올라가는 방법. Parent[x]를 x의 부모 노드라고 할 때 x = Parent[x] 연산을 계속해서 수행하는 것. 단 부모 노드를 구하고자 하는 두 정점의 LEVEL이 다르다면 이 방법으로는 불가능함. 

<br/><br/>

## 2. 아이디어

자신의 부모를 저장할 parent 배열, 자신의 깊이를 저장할 depth 배열이 필요함. 

1. 각 depth에 따른 노드들을 조사함 이를 depth 배열에 저장
2. parent 배열에는 각 노드들의 부모 노드들을 저장함

이 두 배열을 사용해서 두 노드가 주어졌을 때 LCA를 찾을 수 있음

1. depth, parent 배열 조사
2. 아래 의사 코드로 수행
    
    ```
    while(true){
    	if(depth가 일치)
    		if(두 정점의 parent 일치?) LCA 찾음(종료)
            else 두 정점을 자신의 parent 정점 값으로 변경
        else // depth 불일치
            더 depth가 깊은 정점을 해당 정점의 parent 정점으로 변경(depth가 감소됨)
    }
    ```
