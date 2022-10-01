# 📍 계수 정렬 (Count Sort)

계수 정렬은 데이터 값을 직접 비교하지 않고, 단순하게 각 숫자가 몇 개 있는지 개수를 세어 저장한 후에 정렬하는 알고리즘

<br>

## 원리

![image](https://user-images.githubusercontent.com/78673570/193424450-556c8f46-10d7-4eef-8bc8-f28dbb459e34.png)

1. 정렬하고자 하는 배열의 최댓값을 구한다
2. 최댓값 크기의 배열에 각 원소를 순회하며 해당 값이 몇 개 인지 저장한다
3. 저장된 데이터를 순서대로 출력한다


<br>

## 장점

- 크기를 기준으로 개수만 세면 되기 때문에 위치를 변경할 필요가 없다. 
- 데이터 간의 비교가 발생하지 않는다.

<br>

## 단점

- 개수를 저장하는 배열을 사용해야 하기 때문에 추가 공간이 필요하다. 
- 정렬해야할 수의 범위가 클 경우, 엄청난 메모리 낭비가 발생할 수 있다.

<br>

## 구현
```java
int arr[5];
int sorted_arr[5];
int counting[6];

for(int i = 0; i < arr.length; i++){
  counting[arr[i]]++;
}

for(int i = 1; i < counting.length; i++){
  counting[i] += counting[i - 1];
}

for(int i = arr.length - 1; i >= 0; i--){
  counting[arr[i]]--;
  sorted_arr[counting[arr[i]]] = arr[i];
}
```
