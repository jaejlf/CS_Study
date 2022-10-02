# 계수 정렬 (Count sort)

> 주어진 배열의 값 범위가 작은 경우 빠른 속도를 갖는 정렬 알고리즘

최댓값과 입력 배열의 원소 값 개수를 누적합으로 구성한 배열로 정렬을 수행한다.

<br/>
`Օ(n+데이터의 최대값 k)`의 속도가 보장되는 정렬이며, 배열 내에 특정한 값이 몇번 등장했는지에 따라 정렬을 수행하기 때문에 비교연산이 사용되지 않는다.

<br/>

### 계수 정렬 동작 과정

<br/>

<p align="center" style="color:gray">
<img width="402" alt="dirtyRead" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FSlOnN%2Fbtq9VjQhwpB%2FBPgwYs9FZxcoN2OVfDB4Tk%2Fimg.png">
</p>

#### 1. 입력 배열의 최댓값, Counting Array 생성

<br/>

- A: 원 배열
- B: Counting Array, 각 배열의 원소가 몇 번 등장하는지 카운팅하는 배열
- C: Places 배열

<br/>

<p align="center" style="color:gray">
<img width="402" alt="dirtyRead" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcsfq1A%2Fbtq9VkPbkcq%2FiqdisRChqBAKjMs4GCDs0K%2Fimg.png">

</p>

#### 2. Counting

배열을 순회하며 값들의 등장 횟수를 카운팅한다. 만약 같은 값이 나온다면 갱신해준다.

<br/>

<br/>

#### 3. Counting Sum

Counting Array를 1부터 마지막 값까지 바로 이전 값과 계속 더해서 누적합으로 만들어준다.

<p align="center" style="color:gray">
<img width="402" alt="dirtyRead" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fo8pEy%2Fbtq9O7KkZpE%2F2PDddKkmS88aBf1MTl9FK1%2Fimg.png">

#### 4. Sorting

📌 (과정 정리)

- origin 배열을 뒤에서 앞으로 순회.
- origin[i] 값의 누적합에 해당하는 위치에 값을 대입.
- origin[i] 값이 하나 없어졌으므로 해당 값에 대한 누적합을 1 감소.
- 2번과 3번을 반복.

---

<br/>

- A, 즉 원 배열의 가장 뒤에서 부터 값을 하나씩 꺼낸다. 6를 꺼냈기 때문에 이 값을 인덱스로 하여 B, Counting Array에 접근한다.

- B, Counting Array의 6번 인덱스에 있는 값은 6이기 때문에 이 값을 사용해서 C, Places 배열에 접근한다.

- C, Places 배열의 6번째 요소에 6을 넣는다. 원 배열에 6보다 같거나 작은 값이 6개 있기 때문에 Places 배열의 6번째 칸에 넣어주면 6보다 작은 값은 모두 이 인덱스의 앞에 위치하고 큰 값들은 뒤에 위치하게 된다.

- 그 이후 B, Counting Array의 2번 인덱스의 값을 하나 줄여준다.

<p align="center" style="color:gray">
<img width="402" alt="dirtyRead" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbuAzYx%2Fbtq9NROKyTL%2FCRIlZXJd3vlglI7TVHLGv1%2Fimg.png">
</p>

<br/>

### 시간복잡도

배열의 크기를 n, 가장 큰 수를 k라고 하면 계수 정렬의 시간 복잡도는 O(n+k) 입니다.

각각의 수가 몇 개 나왔는지 세는 과정, origin 배열을 역으로 순회하는 과정은 모두 O(n).

그리고 누적합을 구하는 과정이 O(k).

- k가 n보다 작다는 것이 보장된 경우: O(n)
- k가 n보다 크다면 시간 복잡도의 예측이 어려움

<br/>
 
 ## B. 참고자료

🔗 [계수정렬](https://ssungkang.tistory.com/entry/Algorithm-Counting-Sort-%EA%B3%84%EC%88%98-%EC%A0%95%EB%A0%AC)

🔗 [[알고리즘 정리] 계수 정렬(Couting Sort)](https://jeonyeohun.tistory.com/103)
