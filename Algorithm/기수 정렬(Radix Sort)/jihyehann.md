# 💡 기수 정렬(radix sort)

낮은 자리수부터 비교하여 정렬해 간다는 것을 기본 개념으로 하는 정렬 알고리즘.

비교 연산을 하지 않아 정렬 속도가 빠르지만, 데이터 전체 크기에 기수 테이블의 크기만한 메모리를 더 필요로 한다.

<br/>

## 1. 알고리즘

1. 0~9 까지의 Bucket(Queue 자료구조)을 준비한다.
2. 모든 데이터에 대하여 가장 낮은 자리수에 해당하는 Bucket에 차례대로 데이터를 둔다.
3. 0부터 차례대로 버킷에서 데이터를 다시 가져온다.
4. 자리수를 높여가며 2번 3번 과정을 반복한다.

![image](https://user-images.githubusercontent.com/75151848/193444070-88fe8cc5-eb9b-4764-abfa-560512359414.png)

> #### ✔️ LSD 기수 정렬 vs MSD 기수 정렬
> LSD(Least Significant Digit) 기수 정렬
> - 장점 : 구현이 간단하다.
> - 단점 : 마지막까지 결과를 알 수 없다.
> 
> MSD(Most Significant Digit) 기수 정렬
> - 장점 : 끝까지 가지 않아도 중간에 정렬이 완료될 수 있다.
> - 단점 : 중간에 데이터를 점검해야 하기 때문에 구현이 복잡해진다.


<br/>

## 2. 구현 (오름차순)
### Java
```java
import java.io.*;
import java.util.*;

class Radix {

	// A utility function to get maximum value in arr[]
	static int getMax(int arr[], int n) {
		int mx = arr[0];
		for (int i = 1; i < n; i++)
			if (arr[i] > mx)
				mx = arr[i];
		return mx;
	}

	// A function to do counting sort of arr[] according to
	// the digit represented by exp.
	static void countSort(int arr[], int n, int exp) {
		int output[] = new int[n]; // output array
		int i;
		int count[] = new int[10];
		Arrays.fill(count, 0);

		// Store count of occurrences in count[]
		for (i = 0; i < n; i++)
			count[(arr[i] / exp) % 10]++;

		// Change count[i] so that count[i] now contains
		// actual position of this digit in output[]
		for (i = 1; i < 10; i++)
			count[i] += count[i - 1];

		// Build the output array
		for (i = n - 1; i >= 0; i--) {
			output[count[(arr[i] / exp) % 10] - 1] = arr[i];
			count[(arr[i] / exp) % 10]--;
		}

		// Copy the output array to arr[], so that arr[] now
		// contains sorted numbers according to current
		// digit
		for (i = 0; i < n; i++)
			arr[i] = output[i];
	}

	static void radixsort(int arr[], int n) {
		// Find the maximum number to know number of digits
		int m = getMax(arr, n);

		// Do counting sort for every digit. Note that
		// instead of passing digit number, exp is passed.
		// exp is 10^i where i is current digit number
		for (int exp = 1; m / exp > 0; exp *= 10)
			countSort(arr, n, exp);
	}
}
```
<br/>

## 3. 시간복잡도

$O(d*(n+b))$ 의 시간복잡도를 가진다.
- d : 정렬할 숫자의 자릿수
- b : 버킷의 크기. 표현하는 숫자를 기반으로 정해지며, 10진수의 경우 b는 10이다.

<br/>

## 4. 장점

- 안정 정렬(stable sort)이다.
- 문자열, 정수 정렬이 가능하다.

<br/>

## 5. 단점

- 자릿수가 없는 것은 정렬할 수 없다. (ex. 부동소수점)
- 중간 결과를 저장할 bucket 공간이 필요하다.


<br/>

## 🔖 참고
- [Radix Sort](https://www.geeksforgeeks.org/radix-sort/?ref=lbp)
- [기수 정렬(Radix sort)](https://gyoogle.dev/blog/algorithm/Radix%20Sort.html)
