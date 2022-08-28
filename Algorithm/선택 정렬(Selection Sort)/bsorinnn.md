# 선택 정렬(Selection Sort)

> 해당 순서에 원소를 넣을 위치는 이미 정해져 있고, 어떤 원소를 넣을지 선택하는 알고리즘

<br>

방식은 다음과 같다.

1. 데이터 중 가장 작은 값을 찾는다
2. 찾은 값을 데이터 맨 앞 값과 교체한다
3. 맨 앞 데이터를 제외하고 위 과정을 반복한다

<img src="https://cdn.programiz.com/cdn/farfuture/VPGtdVYag2vfHBotOaFEiYLqvWAD_Jwfnwur_AtKQHo/mtime:1582112622/sites/tutorial2program/files/Selection-sort-0.png" height=250>

<br>

<img src="https://miro.medium.com/max/1400/1*5WXRN62ddiM_Gcf4GDdCZg.gif" height=150>

<br>

### 특징

- **장점**
  - 코드가 직관적이여서 구현도 비교적 간단하다
  - 정렬을 위한 비교 횟수는 많으나 교환 횟수는 상당히 적다
- **단점**
  - 안전성을 만족하지 않는다
  - 즉, 값이 같은 레코드가 있는 경우에 상대적인 위치가 변경될 수 있다.

<br>

### 선택 정렬의 시간 복잡도

- Best: `О(n^2)`
- Average: `О(n^2)`
- Worst: `О(n^2)`

<br>

## B. 선택 정렬 Swift로 구현하기

<br>

### Psuedo Code

```Swift
func selsrtI(lst)
    max = length(lst) - 1

    for i from 0 to max
        key = lst[i]
        keyj = i

        for j from i+1 to max
            if lst[j] < key
                key = lst[j]
                keyj = j

        lst[keyj] = lst[i]
        lst[i] = key

    return lst

end func
```
