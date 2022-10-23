# 📍 최장 증가 수열(LIS, Longest Increasing Subsequence)

![image](https://user-images.githubusercontent.com/78673570/197380917-90e5713c-70fe-476b-ae4b-f3b059eff278.png)
![image](https://user-images.githubusercontent.com/78673570/197380930-bec9efbe-7ef2-4915-9724-13cc68d7f686.png)

어떤 수열이 주어질 때 그 수열에서 몇 개의 수들을 제거하여 부분 수열을 만들 수 있는데 그중에서 오름차순으로 정렬된 가장 긴 수열

<br>

## 구현 - DP

- 이중 반복문을 통해 수열의 맨 앞부터, 맨 뒤까지 index를 증가시키며 확인
- 시간 복잡도 : O(N^2)

<br>

```java
for (int k = 0; k < n; k++){
	length[k] = 1;
    for (int i = 0; i < k; i++){
        if(arr[i] < arr[k]){
            length[k] = max(length[k], length[i] + 1);
        }        
    }
}
```
- length[i] : i번째 인덱스에서 끝나는 최장 증가 부분 수열의 길이

<br>

## 구현 - 분할 정복

- 시간 복잡도 : O(nlogn)

![image](https://user-images.githubusercontent.com/78673570/197381161-499e34ec-2a7c-4341-922b-48da8be40fb8.png) 
