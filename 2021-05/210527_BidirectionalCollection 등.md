# 210527

# 학습 내용

- String, Array

# 고민한 점 / 해결 방법

### [BidirectionalCollection]

- String이 채택하고 있으며, Collection 프로토콜을 상속받고 있는 프로토콜이다.
- '양방향성 컬렉션'이라는데 이게 뭘까?
- [https://developer.apple.com/documentation/swift/bidirectionalcollection/](https://developer.apple.com/documentation/swift/bidirectionalcollection/)
- [https://0urtrees.tistory.com/120](https://0urtrees.tistory.com/120)
- 후방, 전방 순회를 둘 다 지원하는 컬렉션 프로토콜
- 마지막 요소(element)를 효율적으로 접근할 수 있도록 하는 기능, 역순으로 요소들을 얻을 수 있게 해주는  reversed(), suffix(_:) 메서드 등이 그 예이다.
- 근데 이 이상으로 이해가 잘 안된다.

### [BidirectionalCollection, MutalbleCollection,  Collection]

- Collection이 다 같은 Collection인줄 알았는데 String은 BidirectionalCollection을, Array는 MutableCollection을, Set과 Dictionary는 Collection을 준수한다.
- 근데 이상하다. MutableCollection은 elements의 값을 변경할 수 있는 Collecion 프로토콜인데 Collection을 준수하는 Dictionary도 Array 처럼 원하는 키의 값을  변경해줄 수 있다. 그러면 Dictionary 는 MutableCollection을 채택하던가, Collection도 값을 변경할 수 있다면  Array도 MutableCollection이 아니라 그냥 Collection을 채택하면 될 것 같은데 굳이 MutableCollection이 있다. 왜 그렇지.
- BidirectionalCollection도 이상하다. Array도 전방, 후방 순회가 가능한데 String만 BidirectionCollection을 채택하고 있다. 구분이 안되고 있는데 왜 굳이 프로토콜을 하나 더 만들어서 쓰는걸까?

### [문자열 보간법 (Interpolation)]

- 보간법이란 알고있는 데이터 값들을 이용하여 모르는 값을  추정하는 한 방법을 말한다. (사전적 정의!)
- 평소에 많이 사용하던 것인데도 용어를 까먹고 있었다..!

```swift
let age = 10
let str = "제 나이는 \(age)살 입니다."
```

# 느낀점

- 빈틈이 이렇게 많다! 오늘 풀리지 않은 의문은 Subscript, 시간복잡도 등을 공부해보고 다시 문서를 봐야겠다.