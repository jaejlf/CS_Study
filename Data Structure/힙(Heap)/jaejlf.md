## 📍 Heap, 힙
![image](https://user-images.githubusercontent.com/78673570/181783838-2507e719-d6df-4336-a099-6abd9f8f9e98.png)

-   이진트리의 일종
-   정렬된 상태가 아니며, 완전 이진 트리와는 다르게 중복값이 허용된다.
-   트리 구조이기 때문에 삽입/삭제는 O(nlogn)으로 매우 빠르다.
-   계산을 편하게 하기 위해, 보통 부모 인덱스는 1부터 시작한다.  
      
    💡 완전 이진 트리  
    1. 마지막 레벨을 제외한 모든 노드가 채워져있어야 한다.  
    2. 모든 노드들은 왼쪽부터 채워져있어야 한다.

<br><br>

## 📍  Min Heap (최소힙)
= 자식 노드가 부모 노드보다 크다

`insert`
1. heap배열의 맨 뒤에 값을 삽입  
2. 삽입한 값의 인덱스가 1보다 크고(= 부모 노드가 존재하고) 부모 노드보다 값이 작으면 → swap  
3. 삽입한 값의 인덱스 /= 2 저장 (노드의 위치가 한칸 올라갔기 때문)

`delete`  
1. heap.size가 비어있으면 리턴  
2. 삭제할 노드는 루트 노드 (= heap.get(1))  
3. 부모 노드에 맨 마지막 값을 저장하고, 맨 마지막 값을 삭제한다.  
4. 부모 노드로부터 최소힙을 재구성한다.
    -   min = 왼쪽 자식 노드 값, minIndex = 왼쪽 자식 노드 인덱스
    -   if, 오른쪽 자식 노드가 있고 && 오른쪽 노드가 왼쪽 자식 노드보다 작으면 → min/minIndex를 오른쪽 노드로 갱신
    -   min 이 부모 노드보다 더 크면, swap 할 필요가 없으므로 종료
    -   min 이 부모 노드보다 작으면 swap

<br>

### 구현

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class min_heap {

    private ArrayList<Integer> heap;

    public min_heap() {

        heap = new ArrayList<>();
        heap.add(0); // 0번째 인덱스 사용 X

    }

    public void insert(int x) {

        heap.add(x);
        int index = heap.size() - 1;

        while (index > 1 && heap.get(index / 2) > heap.get(index)) {

            // swap
            int tmp = heap.get(index / 2);
            heap.set(index / 2, heap.get(index));
            heap.set(index, tmp);

            index = index / 2;
        }

    }

    public int delete() {

        if (heap.size() - 1 < 1)
            return 0;

        int deleteItem = heap.get(1);

        heap.set(1, heap.get(heap.size() - 1));
        heap.remove(heap.size() - 1);

        int index = 1;
        while ((index * 2) < heap.size()) {
            int min = heap.get(index * 2);
            int minIndex = index * 2;

            if (((index * 2 + 1) < heap.size()) && min > heap.get(index * 2 + 1)) {
                min = heap.get(index * 2 + 1);
                minIndex = index * 2 + 1;
            }

            if (heap.get(index) < min)
                break;

            // swap
            int tmp = heap.get(index);
            heap.set(index, heap.get(minIndex));
            heap.set(minIndex, tmp);

            index = minIndex;
        }

        return deleteItem;

    }

    public void printHeap() {

        System.out.println("*** RESULT ***");
        for (int i = 1; i < heap.size(); i++) {
            System.out.print(heap.get(i) + " ");
        }

    }

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());

        min_heap heap = new min_heap();

        for (int i = 0; i < N; i++) {
            int x = Integer.parseInt(br.readLine());

            if (x == 0) {
                System.out.println(heap.delete());
            } else {
                heap.insert(x);
            }
        }

        heap.printHeap();

    }

}
```

<br><br>

## 📍 Max Heap (최대힙)
= 부모 노드가 자식 노드보다 크다

### 구현

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class max_heap {

    private ArrayList<Integer> heap;

    public max_heap() {

        heap = new ArrayList<>();
        heap.add(1000000); // 0번째 인덱스 사용 X

    }

    public void insert(int x) {

        heap.add(x);
        int index = heap.size() - 1;

        while (index > 1 && heap.get(index / 2) < heap.get(index)) {

            // swap
            int tmp = heap.get(index / 2);
            heap.set(index / 2, heap.get(index));
            heap.set(index, tmp);

            index = index / 2;
        }

    }

    public int delete() {

        if (heap.size() - 1 < 1)
            return 0;

        int deleteItem = heap.get(1);

        heap.set(1, heap.get(heap.size() - 1));
        heap.remove(heap.size() - 1);

        int index = 1;
        while ((index * 2) < heap.size()) {
            int max = heap.get(index * 2);
            int maxIndex = index * 2;

            if (((index * 2 + 1) < heap.size()) && max < heap.get(index * 2 + 1)) {
                max = heap.get(index * 2 + 1);
                maxIndex = index * 2 + 1;
            }

            if (heap.get(index) > max)
                break;

            // swap
            int tmp = heap.get(index);
            heap.set(index, heap.get(maxIndex));
            heap.set(maxIndex, tmp);

            index = maxIndex;
        }

        return deleteItem;

    }

    public void printHeap() {

        System.out.println("*** RESULT ***");
        for (int i = 1; i < heap.size(); i++) {
            System.out.print(heap.get(i) + " ");
        }

    }

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());

        max_heap heap = new max_heap();

        for (int i = 0; i < N; i++) {
            int x = Integer.parseInt(br.readLine());

            if (x == 0) {
                System.out.println(heap.delete());
            } else {
                heap.insert(x);
            }
        }

        heap.printHeap();

    }

}
```
