# 💡 비트마스크 (BitMask)

비트마스크란, 집합의 요소들의 구성 여부를 표현할 때 유용한 테크닉을 말한다. 

비트 연산을 통해 부분 집합을 표현할 수 있다.

<br/>

## 1. 사용하는 이유

집합의 요소를 나타낼 때는 보통 배열을 사용하는데 굳이 비트마스크를 사용하는 이유는 무엇일까?

- DP나 순열 등, 배열 활용만으로 해결할 수 없는 문제가 존재한다.
- 작은 메모리와 빠른 수행시간으로 해결이 가능하다. (But, 원소의 수가 많지 않아야 한다)
- 집합을 배열의 인덱스로 표현할 수 있다.
- 코드가 간결해진다.

<br/>

## 2. 비트 연산 (bitwise operation)

1. `&` (and) : 대응하는 두 비트가 모두 1일 때, 1 반환
2. `|` (or) : 대응하는 두 비트 중 모두 1이거나 하나라도 1일때, 1 반환
3. `~` (not) : 비트 값 반전하여 반환 (0 &rarr; 1, 1 &rarr; 0)
4. `^` (xor) : 대응하는 두 비트가 서로 다를 때, 1 반환
5. `<<` (shift left) : `A << B` &rarr; `A*2^B`
6. `>>` (shift right) : `A >> B` &rarr; `A / 2^B`

<br/>

> 활용) 
> - 홀수인지 판별할 때, `if(N % 2 == 1)` 대신 `if(N & 1)` 로 쓸 수 있다.
> - (A+B)/2 대신 `(A+B)>>1` 를 쓸 수 있다.

<br/>

## 3. 비트마스크

### 집합을 정수로 표현

- {1, 3, 4, 5, 9} = 570 = $2^1 + 2^3 + 2^4 + 2^5 + 2^6$ = 1000111010(2)

- 전체 집합 : (1 << N) – 1

- 공집합 : 0

<br/>

### 조회 (포함 여부 확인)

- S 집합에 i가 포함되어 있는지 확인

```
S & (1 << i)

포함하지 않으면 0.
포함하면 0이 아닌 값.
```

### 추가

- S 집합에 i를 추가
- i번째 비트를 1로 만들어주기

```
S | (1 << i)
```

### 제거

- S 집합에서 i를 제거
- i번째 비트를 0으로 만들어주기

```
S & ~(1 << i)
```

### 활용 문제 

- [백준 2098번](https://www.acmicpc.net/problem/2098)
- 외판원 순회 문제 (TSP: Travelling Salesman Problem)
- DP + Bitmask 를 통해 해결할 수 있다.

<br/>

## 4. bitset 라이브러리

bitset 자료구조를 사용하면, 비트마스크를 더 쉽게 나타낼 수 있다.

### Java - java.util.BitSet

[공식 문서](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/BitSet.html)

```java
import java.util.BitSet;

public class BitMasking {
    public static void main(String[] args) {
        BitSet b = new BitSet();
        
        // 추가
        b.set(10);	// 10번째 bit를 true
        b.set(100, true);	// 100번째 bit를 true
        
        // 제거
        b.set(10, false);	// 10번째 bit를 false
       
       	// 조회
        System.out.println(b.get(10));  // false
        System.out.println(b.get(100)); // true
        System.out.println(b.get(0));  // false
    }
}
```

### C++ - <bitset\>

```c
#include <bitset>
#include <string>
#include <iostream> 
using namespace std; 

int main(){    
  // bitset을 선언, 총 10개의 비트를 의미한다.    
  bitset<10> bit;     

  // 전체 비트를 0으로 리셋한다.    
  bit.reset();    

  // 전체 비트를 1로 셋팅한다.    
  bit.set();    

  // 하나라도 1이면 1을 반환, 모두 0이면 0을 반환
  bit.any() ;

  // 모든 비트가 0이면 1 반환
  bit.none();
  
  // 4번째 비트 반전    
  bit.flip(3);      

  // 모든 비트 반전    
  bit.flip();

 
  // 첫 번째 비트는 true, 네 번째 비트는 false 할당    
  bit.set(0, true);    
  bit.set(3, false);     

  // 첫 번째 비트 검사    
  bit.test(0)

  // 다섯 번째 비트 검사(배열형식으로도 가능하다.)    
  bit[4] 


  // 비트를 string으로 변환    
  bit.to_string();    

  // 비트를 숫자(unsigned long)로 변환    
  bit.to_ulong();
} 
```

<br/>

## 🔖 참고
- [gyoogle](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Algorithm/%EB%B9%84%ED%8A%B8%EB%A7%88%EC%8A%A4%ED%81%AC(BitMask).md)
