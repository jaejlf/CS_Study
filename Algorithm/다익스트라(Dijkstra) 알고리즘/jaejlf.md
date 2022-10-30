# 📍 다익스트라(Dijkstra)

![image](https://user-images.githubusercontent.com/78673570/198875682-4c59142c-ee63-4f10-bdec-f6c26f5b36d7.png)

- 다이나믹 프로그래밍을 활용한 대표적인 최단 경로(Shortest Path) 탐색 알고리즘
- 하나의 최단 거리를 구할 때 그 이전까지 구했던 최단 거리 정보를 그대로 사용

<br>

## 동작 원리
1. 출발 노드를 설정한다.
2. 출발 노드를 기준으로 각 노드의 최소 비용을 저장한다.
3. 방문하지 않은 노드 중에서 가장 비용이 적은 노드를 선택한다.
4. 해당 노드를 거쳐서 특정한 노드로 가는 경우를 고려하여 최소 비용을 갱신한다.
5. 위 과정에서 3번 ~ 4번을 반복한다.

<br>

## 예제
0에서 3으로 가는 최단 경로 구하기

<br>

- 각 지점까지의 거리 저장

![image](https://user-images.githubusercontent.com/78673570/198875715-a8702b6b-2a78-4403-8545-452496ebcd04.png)

(cf. 무한대  = 직접적으로 가는 경로가 없는 경우)

<br>

- 표시되어 있는 거리 중 가장 짧은 거리를 S에 추가

![image](https://user-images.githubusercontent.com/78673570/198875751-667d0f16-7211-4fdc-b252-24dcbee8b3f0.png)

새로운 정점이 S에 추가되면, 새로 추가된 정점을 기준으로 다른 정점들의 거리 값이 변경된다.

<br>

- 변경된 정보를 기준으로 다시 갱신 (반복)

![image](https://user-images.githubusercontent.com/78673570/198875831-dda211a9-79bf-4d82-a133-e5f85896ab07.png)
