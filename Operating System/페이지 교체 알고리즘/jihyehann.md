# 💡 페이지 교체 알고리즘 (Page Replacement Algorithm)

페이지 부재(page fault)가 발생하여 새로운 페이지를 할당해야 할 때, 메모리에 빈 프레임이 없는 경우 적재될 페이지를 위해 적재된 페이지 중 어떤 것을 교체해야 한다.

이때 교체 대상을 결정하는 것이 페이지 교체 알고리즘이다.

<br/>

### 1. OPT (Optimal Page Replacement) 알고리즘

"앞으로 참조될 때까지의 시간이 가장 긴 페이지를 교체하는 기법"

![](https://velog.velcdn.com/images/wisdom-one/post/22456e26-73f0-4263-8160-d270effae3ed/image.png)

- 이 기법은 페이지 부재를 최소로 해주는 최적 기법이다.
- 실제로는 앞으로 어떤 페이지들을 참조할지 미리 알 수 없으므로 구현 불가능하다.
- 다른 기법들의 성능 비교의 잣대로써 사용한다.

<br/>

### 2. FIFO 알고리즘

"적재된 지 가장 오래된 페이지를 교체하는 기법"

![](https://velog.velcdn.com/images/wisdom-one/post/2d14d21f-1438-405f-ae91-ef7d78567918/image.png)

- 가장 먼저 적재된 페이지가 교체 대상이다.
- FIFO 모순(Belady's Anomaly) : 페이지 부재율을 낮추기 위해 프레임을 더 많이 주었을 경우 오히려 부재율이 증가하는 현상

<br/>

### 3. LRU (Least Recently Used) 알고리즘

"참조된 지 가장 오래된 페이지를 교체하는 기법"

![](https://velog.velcdn.com/images/wisdom-one/post/efb85562-7bc4-4517-9cef-350ff9d670e3/image.png)

- 미래를 알 수는 없지만, 최근에 자주 참조된 페이지가 앞으로도 당분간 자주 참조될 것이라는 판단에 근거한다.
- 대부분의 시스템에서는 LRU 또는 LRU를 변형시킨 기법이 사용되고 있다.

<br/>


[참고](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Operating%20System/Page%20Replacement%20Algorithm.md)
