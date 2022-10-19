# 💡 이분 탐색 (Binary Search)

## 이분 탐색 (Binary Search) 이란?

"전체 범위를 `이분할` 하여 가운데 값을 비교하여, 두 영역 중 다른 영역으로 이동하여 탐색하는 기법"

- 시간복잡도: $O(logN)$ ( 완전 탐색의 경우 $O(N)$ )
- 전제 조건 : 탐색 전 리스트가 반드시 **정렬되어 있어야 한다.**

<br/>

## 구현 코드

다음은 이분 탐색을 이용하여 배열에서 target 값을 찾아 인덱스를 반환하는 코드이다.

여기서 **배열은 모두 정렬되어 있다고 가정한다.**

### C++

```c
int binarySearch(vector<int>& arr, int target) {
	int left = 0;
    int right = arr.size() - 1;
    
    while (left <= right) {
        int mid = (left + right) / 2;
        if (target == arr[mid]) { // 값 찾음
            return mid; 
        } else if (arr[mid] < target) {
            left = mid + 1;
        } else if (target < arr[mid]) {
            right = mid - 1;
        }
    }
    
    return -1; // 존재하지 않음
}
```


### Java
```java
public static int binarySearch(int[] arr, int target) { 
	int left = 0;
    int right = arr.length - 1;

    while (left <= right) {
        int mid = (left + right) / 2;
        if (target == arr[mid]) { // 값 찾음
            return mid; 
        } else if (arr[mid] < target) {
            left = mid + 1;
        } else if (target < arr[mid]) {
            right = mid - 1;
        }
    }
    
    return -1; // 존재하지 않음
}
```

<br/>

## 라이브러리

### C++ STL

<b> 1. binary_search() - <algorithm\> </b>

`bool binary_search(first, last, target)`

찾는 값이 존재하면 true, 아니면 false를 리턴한다.

```c
#include <iostream>
#include <algorithm>
using namespace std;

int main() {
	int a[10] = {17, 25, 67, 84, 90, 30, 55, 6, 9, 28};
	sort(a, a + 10); // 정렬 - {6, 9, 17, 25, 28, 30, 55, 67, 84, 90}
    cout << binary_search(a, a+10, 55); << endl // 1 (true)
    cout << binary_search(a, a+10, 50); << endl // 0 (false)
    
    return 0;
}
```


<b> 2. lower_bound(), upper_bound() - <algorithm\> </b>

`iterator lower_bound(first, last, target)`
- 주어진 값보다 크거나 같으면서 제일 작은 값을 찾는다. **(값 포함)**

`iterator upper_bound(first, last, target)`
- 주어진 값보다 크면서 제일 작은 값을 찾는다. **(값 미포함)**

```c
#include <iostream>
#include <algorithm>
using namespace std;

int main(){

	int a[10] = {17, 25, 67, 84, 90, 30, 55, 6, 9, 28};
	sort(a, a+10); // 정렬 - {6, 9, 17, 25, 28, 30, 55, 67, 84, 90}

	cout << "lower bound 55: " << *lower_bound(a, a+10, 55) << endl; // 55
	cout << "upper bound 55: " << *upper_bound(a, a+10, 55) << endl; // 67

	cout << "lower bound 80: " << *lower_bound(a, a+10, 80) << endl; // 84
	cout << "upper bound 80: " << *upper_bound(a, a+10, 80) << endl; // 84

	return 0;
}
```

> 공식 문서 참고
> - [binary_search](https://en.cppreference.com/w/cpp/algorithm/binary_search)
> - [lower_bound](https://en.cppreference.com/w/cpp/algorithm/lower_bound)
> - [upper_bound](https://en.cppreference.com/w/cpp/algorithm/upper_bound)

<br/>

### Java

**`Arrays.binarySearch(array, target)`**

- 검색이 일치하는 경우 = 인덱스 번호 반환
- 검색이 일치하는 값이 여러 개인 경우 = 일치하는 인덱스 중 랜덤 반환
- 검색에 실패하는 경우 = -삽입포인트-1 을 반환 <br/>
	즉, 검색에 실패하는 경우 어느 위치에 삽입해야하는지를 간접적으로 알려줌.

```java
import java.util.Arrays;

class BinarySearchTester {
    public static void main(String[] args) {
    	
        int[] arr = {17, 25, 67, 84, 90, 30, 55, 6, 9, 28};
        Arrays.sort(arr); // 정렬 - {6, 9, 17, 25, 28, 30, 55, 67, 84, 90}

        int idx = Arrays.binarySearch(arr, 55);
        System.out.println("반환 인덱스 : "+idx); // 6
        
        idx = Arrays.binarySearch(arr, 66);
        System.out.println("반환 인덱스 : "+idx); // -8 = -7-1
    }
}
```

<br/>

## 참고
- [블로그](https://dev-mystory.tistory.com/m/222)
- [블로그](https://leirbag.tistory.com/m/30)
