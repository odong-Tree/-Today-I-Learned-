# 210529:  Substring

# 학습 내용

- 백준 카이사르 암호
- Substring

<br>

# 고민한 점 / 해결 방법

### [Substring]

- Swift에는 String이 있고 Substring이 있다. Strirng을 다룰 때 어떤  메서드를 사용하면 당연히 Stirng 타입을 반환할 줄 알았는데 Substring을 반환하는 경우가 꽤 많았다. Substring은  무엇이고 왜 필요할까?
- [https://developer.apple.com/documentation/swift/substring/](https://developer.apple.com/documentation/swift/substring/)
- String의  한 부분으로, Substring을 사용할 경우 원본 String과 저장공간을 공유하기 때문에 더 빠르고  효율적이다. 그러니까 Substring이 생겨나더라도 값을 복사하지 않고도 사용할 수 있으며, 값의 복사를 미룰 수 있다. 복사를 미룰 수  있다?
- 만약 Substirng 값을 저장해야한다거나 String 타입의 인스턴스를 요구하는 다른 함수에 값을 전달해주어야할 경우 Substring은 String으로 바뀌게 된다. 이때 `String(_:)` 이니셜라이저를 사용하게  되며 비로소 값이 복사된다. 그러니까 임시적으로 사용하는 경우에는 값 복사가 일어나지 않고, 필요할 때에만 값을 복사하기 때문에 보다 효율적으로 메모리를 사용할 수 있다. 최적화에 유리하다.

---

```swift
// 1.
func test1(str: Substring) {
    print(str)
}

let name1: String = "odongnamu"
test1(str: name1) // error: Cannot convert value of type 'String' to expected argument type 'Substring'

// 2.
func test2(str: String) {
    print(str)
}

let name2: Substring = "odongnamu"
test2(str: name2) // error: Cannot convert value of type 'Substring' to expected argument type 'String'
```

- String과 Substring 서로의 자리에 들어갈 수 없다. 1번은  이해가 되는데 2번의 경우는 이해가 안된다!!
- 그럼 String으로 전달되는 값에서 자동으로 타입이 변경되지 않고 있는 것인데? 무슨 이유일까??????

### [joined()]

- [String] 타입의 Array를 하나의 String으로 합쳐주고  싶었다. 처음에는 reduce라는 고차함수를 이용했다.
- 다른 사람의  풀이를 보니 joined() 메서드로  쉽게 표현해줄  수 있었다.

```swift
let arr = ["O", "d", "o", "n", "g"]
let str = arr.reduce("", { $0 + $1 })

let str2 = arr.joined()
```

<br>

# 느낀점

- 궁금한 걸 알아보다가 또 궁금한게 생기고 또 궁금한게 생긴다. 알아가는 과정이 재밌긴한데 포스팅하다가 궁금한게 꼬리를 무니 쌓여만 있는  글이 많아지고 있다 ..! ㅋㅋ 그래도 조급해 하지말자. 딱 재미가 좋다.