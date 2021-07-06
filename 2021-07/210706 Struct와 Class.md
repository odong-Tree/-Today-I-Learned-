# 210706: Struct와 Class

# 학습 내용

- Struct / Class

<br>

# 고민한 점

### [Struct, Class 언제 무엇을 쓸까..]

- 클래스와 구조체.. 또 고민하게 되었다. 어제 POP의 연장이다. 이 질문에 대해서는 대답을 몇번이나 했었지만 아직도 명쾌하지 않은 것 같다.
- 상속과 참조가 필요한 상황이 아니라면 전반적으로 구조체가 덜 복잡하고 효율적이라고 한다.  동적인 메모리 할당이나 참조 카운팅이 필요가 없고, threadSafe하니까. 상속 같은 경우는 POP가 많이 보완해준다. (만약 class의 멤버로 구조체가 있다면 통째로 참조됨.)
- Objective-C와 연동되는 코드의 경우 @objc 키워드를 사용하기 위해 class를 사용하여 NSObject를 상속받아야한다.
- 데이터의 identity를 제어해야한다면 클래스를 사용하라

### [그러면 UIKit의 객체들은 왜 Class일까?]

- UIKit의 ViewController나 TableView, CollectionView 등은 모두 class로 되어있다. 왜?
- 이유는 NSObject를 상속받아야하기 때문일 것이다. 이까지는 알겠다. 그런데 만약 NSObject를 상속받지 않아도 된다면 Struct로 만들어주었을까?
- SwiftUI는 Struct로 구성된 것들이 많다고 한다.

<br>

### [Struct 안에 Class가, Class 안에 Struct가 있다면?]

- 구글링을 하다가 재밌는 코드를 발견했다.

#### 먼저 클래스 안에 구조체가 있는 경우.

```swift
class classA {
  var booleanInClass = true
  var structInClass = StructInClass()
}
 
struct StructInClass {
  var booleanInStruct = true
}
 
var instance1 = classA()
var instance2 = instance1
 
instance2.structInClass.booleanInStruct = false
instance2.booleanInClass = false
 
print(instance1.booleanInClass)  // false
print(instance1.structInClass.booleanInStruct) // false
```

- 클래스 자체가 Reference 타입으로, 하나의 주소값에 대한 수정이 일어나기 때문에 클래스 변수에 대한 수정은 당연히 반영된다.

#### 구조체 안에 클래스가 있는 경우

```swift
struct StructA {
  var booleanInStruct = true
  var classInStruct = ClassInStruct()
}
 
class ClassInStruct {
  var booleanInStruct = true
}
 
var instance1 = StructA()
var instance2 = instance1
 
instance2.booleanInStruct = false
instance2.classInStruct.booleanInStruct = false
 
print(instance1.booleanInStruct) // true
print(instance1.classInStruct.booleanInStruct) // false
```

- 구조체는 Value 타입으로 복사가 일어나기 때문에 booleanInStruct 변수의 변경이 반영되지 않을 것은 쉽게 예상할 수 있었다.
- 하지만 클래스 타입의 변수는 값타입인 구조체의 멤버이지만 참조가 일어나기 때문에 값이 변경이 반영된다.

<br>

# 느낀점

- 단번에 이해되지 않아서 반복되고 있는 고민이지만 다루어줄 수록 조금씩 더 알아가는 것 같다.
- Struct 안에 Class가 있는 경우에도 참조가 일어나서 값의 변경이 반영된다는 사실이 생소했다. 아무 생각없이 써왔던 것 같다. Value 타입과 Reference 타입의 차이에 대해서 인지했으나 실질적으로 적용되는 코드를 다루어볼 기회는 없었던 것 같다. 새로운 눈이 또 생긴 것 같다.

<br>

### 참고

- [https://abhimuralidharan.medium.com/difference-between-a-struct-and-a-class-in-swift-53e08df73714](https://abhimuralidharan.medium.com/difference-between-a-struct-and-a-class-in-swift-53e08df73714)
- [https://developer.apple.com/documentation/swift/choosing_between_structures_and_classes](https://developer.apple.com/documentation/swift/choosing_between_structures_and_classes)
- [https://macgongmon.club/27](https://macgongmon.club/27)
