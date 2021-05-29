# 210528: enuarated, 알파벳

# 학습 내용

- 코딩 테스트 문제 풀기
- 'String은 왜 Array처럼 사용할 수 없을까?' 포스팅 작성 (하지만 공부가 더 필요!! ㅜ)

<br>

# 고민한 점 / 해결  방법

### [enumarated]

- array를  돌면서 각 elements와 index 값을 같이 다루어 주고 싶다면? enumarated를 사용할  수 있었다.
- [https://developer.apple.com/documentation/swift/array/1687832-enumerated](https://developer.apple.com/documentation/swift/array/1687832-enumerated)

```swift
let arr = [10, 20, 30, 40, 50, 60, 70]
for (index, num) in arr.enumerated() {
    print("index: \(index), num: \(num)")
}

*/
출력
index: 0, num: 10
index: 1, num: 20
index: 2, num: 30
index: 3, num: 40
index: 4, num: 50
index: 5, num: 60
index: 6, num: 70
/*
```

### [알파벳 Array로 만들기]

- ["A", "B", "C", ..., "Z"] 하나씩 적어주는 방법 말고 더 간단한 방법은 없을까?
- String을 배열로  바꾸어주기, Int 범위로 UnicodeScalar로  변환하기 등의 방법이 있었다.

```swift
var alphabetArray = Array("ABCDEFGHIJKLMNOPQRSTUVWXYZ").map{ String($0) }
let alpabet = Array(65 ... 90).map{ String(UnicodeScalar($0)!) }
```

- 그럼 둘 중에 뭐가 더 빠를까? 뭐가  더 효율적일까
- 라이노님이 공유해준 링크: [https://stackoverflow.com/questions/49808837/initialize-a-string-from-a-range-of-characters-in-swift](https://stackoverflow.com/questions/49808837/initialize-a-string-from-a-range-of-characters-in-swift)

<br>

# 느낀점

- 코딩 테스트를 풀어보며 내가 Swift를 아직 잘모르는구나하는 생각이 든다. 다른  사람이  제출한  코드를 보면서  많은 공부가 되고 있다.
- 'String은 왜 Array처럼 사용할 수 없을까?'라는 주제로  포스팅을 작성하고 있는데 아직 모르는 부분이  많아서  작성하기가 어렵다. 유니코드, UTF도 아직 잘 모르겠고,  Array의 각 index 메모리를 이해하는데에 C언어의 포인터 개념이 필요한데 이 부분도  잘 모르겠다. 짬짬이 시간내어서 부스트코스의 CS기초 (C언어) 강의를 들어봐야겠다.
