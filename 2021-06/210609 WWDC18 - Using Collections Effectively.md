# 210609: WWDC18 - Using Collections Effectively

# 학습 내용

- [WWDC18 - Using Collections Effectively](https://developer.apple.com/videos/play/wwdc2018/229)
- Instruments, Memory

<br>

### [Bidirectional Collection, Random Access Collection]

- Collection 프로토콜에도 여러가지가 있다.
- Bidirectional Collection: forward 말고 다른 방향으로도 인덱스 서칭이 가능, index(after:), index(before:) 메서드 둘 다 사용 가능
- random access collection: 무작위로 인덱스에 접근이 가능 → O(1)으로 양방향 컬렉션에 비해 효율적인 접근이 가능하다.

### [Bridging]

- Swift의 Array는 구조체로 값 타입, Objective-C의 NSArray는 클래스로 참조 타입이다. 따라서 메모리를 차지하는 방법이 다르다. 그런데 이  둘은 bridging 되어있다. (두 언어를 호환시키기 위해서)
- 두 언어간의 브릿징을 할 때에는 항상 비용이 발생한다. 한 언어로 공간을 차지한 후에 다른 언어로도 공간을 차지한다. 즉 변환 과정이 필요한 것. 이는 때로 재귀적일 수 있는데 문자열 배열의 경우 배열로서 브릿징이 먼저 이루어지고 각 문자열의 브릿징이 일어난다.
- 브릿징에는 두 가지 방식이  있는데, 예를 들어 `Array<Data> → NSArray<NSData *> *` 와 같이 Collection과 elements 모두 브릿징이 필요한 경우에는 바로바로 브릿징이 이루어지고, `Array<NSView> -> NSArray<NSView *> *` 와 같이 Collection 만 브릿징이 필요한 경우에는 lazy 하게 Collection이 사용되기 전까지 브릿징이 이루어지지 않는다. (NSView와 View는 브릿징하고 있지 않음)

![Untitled](https://user-images.githubusercontent.com/73867548/121421155-d3cc4380-c9a8-11eb-9a32-43a26fd5d55a.png)

![Untitled 1](https://user-images.githubusercontent.com/73867548/121421167-d5960700-c9a8-11eb-981f-9a932f2dbfcf.png)

![Untitled 2](https://user-images.githubusercontent.com/73867548/121421179-d7f86100-c9a8-11eb-99d4-80a950208b36.png)


- 브릿징을 줄이면 실행 시간을 단축시킬 수 있다.

<br>

# 느낀점

- WWDC가 흥미롭다. 안다고 생각한 것도 WWDC로 보니 내가 아는게 아니었구나 싶다. 초반에는 집중이 안돼서 힘들었는데 꾸역꾸역 한 세션을 공부해보니 WWDC와 훨씬 가까워진 것 같다. 앞으로도 자주 애용해야겠다.
- 앱의 메모리를 측정하기 위해서 Profiling에 대해 찾아보다가 Instruments를 접하게 되었다. 단 시간에 익힐 수는 없었다. 내일은 생일이니 쉬엄쉬엄 잘 보내고 다시 공부해봐야지.
