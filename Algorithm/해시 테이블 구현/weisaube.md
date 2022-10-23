# 해시 테이블 구현

## 📌 A. 해시 테이블(Hash Table)

<br/>

> 해시 테이블에서는 "Key"로 object를 저장하고 불러올 수 있다.

<br>

- 해시 테이블은 dictionary나 map, 연관 배열(associate array)를 구현할 때 사용한다.

<br/>

+) 내부적으로 해시 테이블을 사용하기 때문에 Swift의 `Dictionary` Type에서는 Key가 `Hashable` 프로토콜을 상속받아야 한다.

<br/>

### 원리

<br/>

<p align="center">
  <img src="https://velog.velcdn.com/images%2Fyuns_u%2Fpost%2F7a9865f1-c9ab-4984-a5bd-a6eb40a5355f%2Fimage.png" alt="text" width="485" />
</p>

해시 테이블은 `키(Key)`, `해시 함수(Hash Function)`, `해시(Hash)`, `값(value)`, `저장소(Bucket, slot)`으로 이루어져 있다.

- 키(key): 고유한 값이며 해시 함수의 Input
- 해시 함수(hash function): 키를 해시로 바꿔주는 역할
- 해시(hash)
  해시 함수의 결과물이며, 저장소(bucket, slot)에서 값(value)과 매칭되어 저장된다.
- 값(value)
  저장소(bucket, slot)에 최종적으로 저장되는 값으로 키와 매칭되어 저장, 삭제, 검색, 접근이 가능해야 한다.

<br/>

<p align="center">
  <img src="https://velog.velcdn.com/images%2Fhansangjin96%2Fpost%2Ff8870769-7c7c-413f-962b-c6ef21d46b23%2Fimage.png" alt="text" width="485" />
</p>

<br/>

특정 키값을 해시 테이블에 넣으면 Hash Function을 이용해 계산된 값을 배열의 index에 저장한다.

<br/>

```Swift
hashTable["firstName"] = "Steve"
```

<br/>

해시테이블은 `"firstname"` 이라는 키를 가지고 이의 `hashValue` 프로퍼티를 찾는다.

<p align="center">
  <img src="https://velog.velcdn.com/images%2Fhansangjin96%2Fpost%2F268862be-4b00-4547-a006-c959f5c9625b%2Fimage.png" alt="text" width="485" />

<br/>

`"firstName".hashValue` 값을 사용하면 bing integer인 ` -4799450059917011053`를 리턴한다.(이 값은 다를 수 있다.)

<br/>

이런 hashValue를 생성하는 hash Function은 다음과 같이 만들 수 있다.

```Swift
// sourced from https://gist.github.com/kharrison/2355182ac03b481921073c5cf6d77a73#file-country-swift-L31
func djb2Hash(_ string: String) -> Int {
  let unicodeScalars = string.unicodeScalars.map { $0.value }
  return unicodeScalars.reduce(5381) {
    ($0 << 5) &+ $0 &+ Int($1)
  }
}

djb2Hash("abc") // outputs 193485963
djb2Hash("bca") // outputs 193487083
```

<br/>

+) 실제 Swift Standard Library에서 사용하는 hash function은 이것보다 훨씬 더 복잡하며, `SipHash` 알고리즘을 사용한다.

<br/>

## B. 📌 해시 테이블 구현하기

<br/>

```Swift
// sourced from https://github.com/raywenderlich/swift-algorithm-club/tree/master/Hash%20Table

public struct HashTable<Key: Hashable, Value> {
  private typealias Element = (key: Key, value: Value)
  private typealias Bucket = [Element]
  private var buckets: [Bucket]

  private(set) public var count = 0

  public var isEmpty: Bool { return count == 0 }

  public init(capacity: Int) {
    assert(capacity > 0)
    buckets = Array<Bucket>(repeatElement([], count: capacity))
  }
```

<br/>

- `Element`: chain에서 사용할 key/value 페어
- bucket: 저장소

+) 주어진 키로 array index 계산하는 Helper method

<br/>

```Swift
  private func index(forKey key: Key) -> Int {
    return abs(key.hashValue % buckets.count)
  }
```

<br/>

- 해시 테이블의 기능
  - 저장(insertion)
  - 삭제(deletion)
  - 검색(look up)
  - 변경(update)

<br/>

```Swift
hashTable["firstName"] = "Steve" // insert
let x = hashTable["firstName"] // lookup
hashTable["firstName"] = "Tim" // update
hashTable["firstName"] = nil // delete

```

<br/>

Swift에서는 이를 서브스크립트(Subscript)를 이용하여 구현할 수 있다.

<br/>

(+ subscript: subscript 키워드로 작성하며 하나 이상의 파라미터와 반환 값을 지정한다

파라미터나 리턴형을 생략할 수 없고, getter와 setter 모두 구현할 수 있다.)
(출처: 개발자 소들이)

<br/>

```Swift
  public subscript(key: Key) -> Value? {
    get {
      return value(forKey: key)
    }
    set {
      if let value = newValue {
        updateValue(value, forKey: key)
      } else {
        removeValue(forKey: key)
      }
    }
  }
```

<br/>

#### `value`

```Swift
  public func value(forKey key: Key) -> Value? {
    let index = self.index(forKey: key) // bucket 넘버가 나옴
    // collision 발생 시 chaining으로 해결했다면 버켓에 키가 하나 이상 있을 수 있으므로 순회
    for element in buckets[index] {
      if element.key == key {
        return element.value
      }
    }
    return nil  // key not in hash table
  }
```

<br/>

### updateValue

```Swift
  public mutating func updateValue(_ value: Value, forKey key: Key) -> Value? {
    let index = self.index(forKey: key)

    // Do we already have this key in the bucket?
    for (i, element) in buckets[index].enumerated() {
      if element.key == key {
        let oldValue = element.value
        buckets[index][i].value = value
        return oldValue
      }
    }

    // This key isn't in the bucket yet; add it to the chain.
    buckets[index].append((key: key, value: value))
    count += 1
    return nil
  }
```

<br/>

### remove value

```Swift
  public mutating func removeValue(forKey key: Key) -> Value? {
    let index = self.index(forKey: key)

    // Find the element in the bucket's chain and remove it.
    for (i, element) in buckets[index].enumerated() {
      if element.key == key {
        buckets[index].remove(at: i)
        count -= 1
        return element.value
      }
    }
    return nil  // key not in hash table
  }

```

## 📌 C. 참고자료

🔗 [https://www.raywenderlich.com/206-swift-algorithm-club-hash-tables](https://github.com/raywenderlich/swift-algorithm-club/tree/master/Hash%20Table)

🔗 [Hash Table(기본 해시함수 예제, 해시충돌부터)](https://velog.io/@yuns_u/Hash-Table%EA%B8%B0%EB%B3%B8-%ED%95%B4%EC%8B%9C%ED%95%A8%EC%88%98-%EC%98%88%EC%A0%9C-%ED%95%B4%EC%8B%9C%EC%B6%A9%EB%8F%8C%EB%B6%80%ED%84%B0)
