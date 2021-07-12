# 210712: closure self

# Closure에서는 왜 self를 사용할까?

### [Capture List]

```swift
var a = 0
var b = 0
let closure = { [a] in
    print(a, b)
}

a = 10
b = 10
closure()
// Prints "0 10"
```

### capture list를 왜 사용할까?

- 순환 참조 문제와 객체의 값만 복사해서 사용하기 위해서 사용한다.

### 1. 순환 참조 해결

```swift
// 순환 참조
class TestRetainCycle {
    var property: String = ""
    var comletionHandler: ()->() = {}

    func occurRetainCycle() {
        comletionHandler = {
            print(self.property)
        }
    }
}

```

- property 라는 프로퍼티에 대해서 순환참조가 일어나는 것을 capture list로 해결해줄 수 있다.
- 아래와 같이 순환참조가 발생하고 있다.

![image](https://user-images.githubusercontent.com/73867548/125304655-b9e79d00-e368-11eb-9acf-54002689164f.jpeg)


```swift
// capture list
class TestRetainCycle {
    var property: String = ""
    var comletionHandler: ()->() = {}

    func occureRetainCycle() {
        comletionHandler = { [weak self] in
            print(self?.property as Any)
        }
    }
}
```

![image](https://user-images.githubusercontent.com/73867548/125304655-b9e79d00-e368-11eb-9acf-54002689164f.jpeg)


<br>

### 2. 값 복사

```swift
func testCaptureList1() {
    var count = Int(0)
    
    let closure = {
        print("closure:",  count))
    }
    count = 10
    
    closure()
    print("count:", count)
   }
   // 결과
   // closure: 10
   // count: 10

func testCaptureList2() {
    var count = Int(0)
    
    let closure = { [captureCount = count] in
      print("closure:", captureCount)
    }
    count = 10
        
    closure()
    print("count:", count)
}
// 결과
// closure: 0
// count: 10
```

- 처음 예시 코드처럼 값을 capture 해주기 위해서 사용한다.

### 다시, closure에는 왜 self 키워드를 사용해야 할까?

- class 안에서 closure를 생성할 때 암묵적으로 self가 캡처 리스트에 들어가게 된다.
- 따라서 closure에서는 instance의 프로퍼티에 바로 접근할 수 없고 capture list에 자동으로 추가된 self를 통해서 접근해야한다.

<br>

### 참고

- [https://docs.swift.org/swift-book/ReferenceManual/Expressions.html#ID544](https://docs.swift.org/swift-book/ReferenceManual/Expressions.html#ID544)
- [https://docs.swift.org/swift-book/LanguageGuide/AutomaticReferenceCounting.html#ID56](https://docs.swift.org/swift-book/LanguageGuide/AutomaticReferenceCounting.html#ID56)
- [https://eastjohntech.blogspot.com/2019/12/closure-self.html](https://eastjohntech.blogspot.com/2019/12/closure-self.html)
