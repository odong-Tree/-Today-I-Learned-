# 210608: Dictionay 고차함수

# 학습 내용

- Dictionary, 고차함수
- WWDC 2021

<br>

# 고민한 점 / 해결 방법

### [Dictionary, 고차함수 다루기]

```swift
var dic = [1: 10, 2: 20, 3: 30, 4: 40, 5: 50]

let arr1 = dic.map { key, value -> Int in
    return value
}
print(arr1) // [50, 10, 20, 40, 30]

let arr2 = dic.map { (key, value) -> Int in
    return key + value
}
print(arr2) // [55, 11, 22, 33, 44]
// 항상  [T] 배열로 반환이 된다. 즉, dictionary를 map해서 새로운 dictionary로 만들 수는 없다..!!

let arr3 = dic.sorted(by: >)
print(arr3) // [(key: 5, value: 50), (key: 4, value: 40), (key: 3, value: 30), (key: 2, value: 20), (key: 1, value: 10)]
print(arr3.map{ $0.key }) // [5, 4, 3, 2, 1]

//let arr4 = dic.sorted { dic1, dic2 -> Bool in
//    return dic1.value > dic2.value
//}
let arr4 = dic.sorted { $0.value > $1.value }
print(arr4)
print(arr4.map{ $0.key })

let arr5 = dic.reduce(0) { $0 + $1.value }
//let arr4 = dic.reduce(<#T##initialResult: Result##Result#>, <#T##nextPartialResult: (Result, (key: Int, value: Int)) throws -> Result##(Result, (key: Int, value: Int)) throws -> Result#>)
print(arr5) // 150
// $0.value + $1.value가 아니라, $0 + $1.value로 연산해주어야 한다. $0은 반환되는 타입, 순차적인 계산 결과이기 때문.

let some = dic.filter { $0.value > 24 }
print(some) // [5: 50, 4: 40, 3: 30]
// filter는 dictionary 타입 그대로 뽑힌다.
```

- Dictionary를 sorted하면 tuple의 배열로 나오는구나.

### [lazy collection?]

![Untitled](https://user-images.githubusercontent.com/73867548/121421032-b4351b00-c9a8-11eb-907b-722ed3545808.png)


- [WWDC18 - Using Collections Effectively](https://developer.apple.com/videos/play/wwdc2018/229)
- [https://www.avanderlee.com/swift/lazy-collections-arrays](https://www.avanderlee.com/swift/lazy-collections-arrays/)

```swift
let usernames = ["Antoine", "Maaike", "Jaap", "Amber", "Lady", "Angie"]
 usernames
     .filter { username in
         print("filtered name")
         return username.lowercased().first == "a"
     }.forEach { username in
         print("Fetch avatar for (username)")
     }
 /*
  Prints:
  filtered name
  filtered name
  filtered name
  filtered name
  filtered name
  filtered name
  Fetch avatar for Antoine
  Fetch avatar for Amber
  Fetch avatar for Angie
  */

// lazy
let usernames = ["Antoine", "Maaike", "Jaap", "Amber", "Lady", "Angie"]
 usernames.lazy
     .filter { username in
         print("filtered name")
         return username.lowercased().first == "a"
     }.forEach { username in
         print("Fetch avatar for (username)")
     }
 /*
  Prints:
  filtered name
  Fetch avatar for Antoine
  filtered name
  filtered name
  filtered name
  Fetch avatar for Amber
  filtered name
  filtered name
  Fetch avatar for Angie
  */
```

- 근데 이상하게 .first가 아니라 인덱스로 접근하면 lazy filter가 정상적으로 호출되지 않는다. LazyFilterSequence나 LazyMapSequence 구조체처럼 LazySequenceProtocol을 준수하는 타입의 메서드에만 정상적으로 동작하는 것 같다.

<br>

# 느낀점

- 새벽에 잠드는 바람에 아침에 WWDC를 보게 되었다. 오랜만에 디스코드에서 캠퍼들과 보고싶었는데 ㅜ.. 아주아주 큰 변화나 신제품에 대한 소식은 없어서 아쉽기는 했지만 이렇게 금방금방 기술이 발전하는게 신기하다.
- iOS15 에서는 FaceTime  기능이 강화되었다. Zoom과 유사한 기능들을 지원하고, 안드로이드와 호환도 가능해진다고 한다. 화면 공유 기능은 내가 개발해보고 싶은 기능이었는데 FaceTime에서 쉽게 사용이 가능해졌다..! 이번 WWDC에서 가장 인상적이었던 것은 새로운 MacOS  Monterey에서 가능한 Universal Control 기능이다. 연동없이 맥, 아이패드, 아이맥에서 커서가 자유롭게 넘나들 수 있다니..!
