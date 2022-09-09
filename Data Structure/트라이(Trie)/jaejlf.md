# 📍 트라이 (Trie)

![image](https://user-images.githubusercontent.com/78673570/189361741-859f5494-2aeb-4ba3-9b68-b12ef9f6d14f.png)

- 문자열에서 검색을 빠르게 도와주는 자료구조
- 트리의 루트에서부터 자식들을 따라가면서 생성된 문자열들이 트라이 자료구조에 저장되어있다고 할 수 있다.
- 정수형에서 이진탐색트리를 이용하면 시간복잡도는 `O(logN)`
- 하지만 문자열에서 적용했을 때, 문자열 최대 길이가 M이면 `O(M*logn)`이 된다.
- 트라이를 활용하면 `O(M)`으로 문자열 검색이 가능하다.

<br>

## 구현

```java
static class Trie {
    boolean end;
    boolean pass;
    Trie[] child;

    Trie() {
        end = false;
        pass = false;
        child = new Trie[10];
    }

    public boolean insert(String str, int index) {
        if(end) return false;
        if(index == str.length()) {
            end = true;
            if(pass) return false;
            else return true;
        }
        else {
            int next = str.charAt(index) - '0';
            if(child[next] == null) {
                child[next] = new Trie();
                pass = true;
            }
            return child[next].insert(str, index + 1);
        }

    }
}
```
