# 210621: "HH:mm", TimeInterval

# 학습 내용

- 프로그래머스 올바른 괄호
- 프로그래머스 방금그곡

# 고민한 점 / 해결 방법

### [시간 계산하기]

- "HH:mm" 형식의 시간에서 두 시간의 차를 분 단위로 연산 해야했다.

![Untitled](https://user-images.githubusercontent.com/73867548/122852250-47783400-d34b-11eb-9893-d9607cd05d07.png)

- Date 타입은 Date끼리 직접 덧셈 뺄셈 연산이 불가능하다.
- TimeInterval을 분  단위로 구할 수 있으면 좋겠다.

![Untitled 1](https://user-images.githubusercontent.com/73867548/122852257-49da8e00-d34b-11eb-932d-04cbd20fad76.png)

- 이  메서드로 Double 타입의 TimeInterval을 구할 수 있다.

```swift
let start = "13:00"
let end = "13:08"

let format = DateFormatter()
format.dateFormat = "HH:mm"
let s = format.date(from: start)!
let e = format.date(from: end)!

let interval = e.timeIntervalSince(s) / 60
print(interval) // 8.0

// Int(interval)
```

# 느낀점

- 코드를 작성하긴 했는데 어느 포인트에서 에러가 나는지 모르겠다. 예시를 잘 만들 필요가 있어보이는데. 내일 다시 여러 테스트를 해보자
- Date 타입에 대해서 한 번 포스팅을 해야겠다. 자꾸 찾아보게 된다.
