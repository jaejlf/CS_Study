# 💡 트라이(Trie)

## 1. 정의

**트라이(Trie)** 란?

문자열 검색을 빠르게 해주는 이진 탐색 트리를 말한다.

일반적인 이진 탐색 트리를 이용하면, 최대 길이가 M인 문자열 검색 시 $O(MlogN)$ 의 시간복잡도가 걸린다.
그러나 트라이를 이용하면 $O(M)$으로 문자열 검색이 가능하다.

![](https://velog.velcdn.com/images/wisdom-one/post/8145b742-0076-4f92-9f47-41c0c2f626a4/image.png)

<br/>

## 2. 구현

```java
public class TrieNode {
    private HashMap<Character, TrieNode> children;
    private String content;
    private boolean isWord;
    
   // ...
}

public class Trie {
    private TrieNode root;
    //...
    
    // 삽입
    public void insert(String word) {
        TrieNode current = root;

        for (char l: word.toCharArray()) {
            current = current.getChildren().computeIfAbsent(l, c -> new TrieNode());
        }
        current.setEndOfWord(true);
    }
    
    // 검색
    public boolean find(String word) {
        TrieNode current = root;
        for (int i = 0; i < word.length(); i++) {
            char ch = word.charAt(i);
            TrieNode node = current.getChildren().get(ch);
            if (node == null) {
                return false;
            }
            current = node;
        }
        return current.isEndOfWord();
    }
    
    // 삭제
    public void delete(String word) {
        delete(root, word, 0);
    }

    private boolean delete(TrieNode current, String word, int index) {
        if (index == word.length()) {
            if (!current.isEndOfWord()) {
                return false;
            }
            current.setEndOfWord(false);
            return current.getChildren().isEmpty();
        }
        char ch = word.charAt(index);
        TrieNode node = current.getChildren().get(ch);
        if (node == null) {
            return false;
        }
        boolean shouldDeleteCurrentNode = delete(node, word, index + 1) && !node.isEndOfWord();

        if (shouldDeleteCurrentNode) {
            current.getChildren().remove(ch);
            return current.getChildren().isEmpty();
        }
        return false;
    }
}
```

<br/>

## 3. 시간복잡도

문자열의 최대 길이가 M일 때, 검색, 삽입, 삭제 모두 $O(M)$ 시간에 수행된다.

<br/><br/>

## 🔖 참고
- [Trie](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Data%20Structure/Trie.md)
- [Trie 구현](https://www.baeldung.com/trie-java)
