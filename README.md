
## 묵찌빠게임 프로젝트

#### 기간 
2021.10.11 - 2021.10.15 (with 아샌)


## 목차
- [Flow Chart](#플로우-차트)
- [작동 모습](#작동-모습)
- [문제점/해결방법](#문제점과-해결방법)
- [브랜치 전략](#브랜치-전략)

## 플로우 차트

<img src="https://github.com/ICS-Asan/ios-rock-paper-scissors/blob/step2/FlowChart.png" width=50% height=50%/>

- step1
  - 게임 문구 출력
  - 컴퓨터의 패 할당
  - 사용자 입력
  - 입력값 판단
    1) 잘못된 입력
    2) 게임 종료
    3) 게임 승패
  - 입력값 판단 결과 출력(입력 오류, 게임 결과, 종료)

## 작동 모습

![ㄴㄴㄴㄴ](https://user-images.githubusercontent.com/74536728/137576529-2200d8f6-e89f-4aa9-adec-78fd9df75fcf.gif)



## 문제점과 해결방법

### 🔎 하드코딩에 대한 고민
- 아래 코드처럼 코드 중간중간에 매직넘버나 매직 리터럴이 날것으로 존재하는 문제가 있었다
```swift
 func generateComputerNumber() -> Int {
    let number: Int = Int.random(in: 1...3) //이 부분 
    return number
 }
```
하드코딩을 했을때 문제점
1. 모아서 관리하기 어렵다
2. 변경사항이 있을때 반영하기 어렵다
3. 코드를 처음보는 사람이라면 해당 숫자들이 어떤 숫자인지 알기 어렵다
4. 가독성이 떨어진다
  

#### 이에 대한 조언
> 라이언
> - 무엇이 더 중요한지를 생각하보자 (성능인가? or 코드를 작성하는 사람의 편의성인가?)
> - 여러 다른 함수에 하나의 상수를 쳐다보도 있는게 좋을 수도 있다
> - 상수는 메모리에 거의 영향을 주지 않는다

> 네프
> - 전역상수로 선언하되 전역상수들을 관리하는 방법들을 알아보자
> - 스위프트에서는 보통 enum으로 namespace 만들어서 전역상수를 관리한다
> - 대신 한 타입 안에서 사용되는 상수라면 private let 이런식으로 접근제어를 통해 상수를 관리할 수 있을 것이다

<br>

#### 해결방법
`CaseIterable` 프로토콜을 채택해서 randomElement() 메서드로 랜덤사인을 만들어주는 방법으로 해결했다
```swift
  let computer = RockScissorsPaperSign.allCases.randomElement()! 
```  

<br>

#### 위 방법 외에 코드 위에서 날것으로 돌아다니는 매직넘버/매직리터럴을 관리하는 방법

- 전역상수로 전역상수 관리하기
```swift
let validInputs = ["0", "1", "2", "3"]
```

- 케이스가 없는 enum으로 namespace를 만들고 열거형에서 전역상수 관리하기 
```swift
enum GameMessages {
    static let turnGameStart = "가위(1), 바위(2), 보(3)! <종료: 0>: "
}
```  
<br>

#### 정리하자면
1. 다른 어떤 방법으로 매직넘버를 없애거나
2. 타입안에서 전역상수로 선언후 private 같은 접근제어자로 관리
3. 케이스가 없는 enum에서 타입 프로퍼티로 선언해서 관리 하는 방법이 있다
앞으로 2,3번 방법이 어떤 경우에서 쓰이는게 적절할지 그 기준을 만들어봐야겠다

<br>

## 🔎 함수의 이름에 대한 고민

컴퓨터의 패를 정하는 함수의 이름을 `getComputerSign` 이라고 지었는데  
보통 함수 이름에 get 을 잘 사용하지 않는다고 한다  
-> 우리처럼 값을 할당하는 함수라면 set을 사용하용하는것이 좋을것 같다

#### 결론
- 함수를 사용하는 사람은 "어떤 input을 넣었을때 -> 어떤 결과가 나온다" 만 중요하다  
- 내가 함수를 사용하는 입장에서 다시 한번 생각해보자

<br>

## RawValue의 의미
- 아래 코드에서 열거형의 케이스에 Int 값을 직접 할당하는게 적절한가? 아니다   
- rawValue는 해당 case와 완전히 짝지을 수 있는 값이어야 한다  

```swift 
enum Sign: Int {
    case rock = 1
    case scissors = 2
    case paper = 3
}
```
<br>

#### 해결방법
- 원시값을 주기보단 이니셜라이저를 만들고 input을 받아 인스턴스를 생성하는 방법으로 해결했다
```swift
init?(input: Int) {
        switch input {
        case 1:
            self = .rock
        case 2:
            self = .scissors
        case 3:
            self = .paper
        default:
           return nil
        }
    }
```


<br>

## 🔎 nil-coalescing operator의 사용

아래 코드에서 `??` 를 사용하는 것이 적절한가?

```swift
func receivePlayerInput() -> String {
    let playerInput = readLine() ?? ""
    return playerInput
}
```
- 위 코드를 작성할 때 왜 readLine의 리턴타입이 optional 인지 정확히 알아보지 않았다.  
- 따라서 nil값이 나오지 않을것 이라고 예상했고, 항상 값이 있으니 ??를 사용해도 상관이 없을거라고 예상했는데  
- 공식문서를 읽어보니 EOF일때 readline의 리턴값이 nil일 수 있다고 한다.  
- (EOF란 데이터 소스로부터 더 이상 읽을 수 있는 데이터가 없음을 나타낸다고 합니다)  

- 이렇게 에러가 발생했을 때 empty string을 리턴하는것은 적절하지 않다  

<br>

#### 해결방법
- readLine으로 사용자 입력을 받을 때 만약 nil이 리턴된다면 throw로 오류를 던지도록 수정했다  
```swift
func receivePlayerInput() throws -> String {
    guard let playerInput = readLine() else {
        throw InputError.invalidInput //nil 일때 invalidInput오류를 던짐
    }
    return playerInput
}
```

<br> 

## 🔎 길지만 이해하기 쉬운코드 vs 짧고 빠르지만 이해하기 어려운 코드
- 처음에 승패를 판단하는 함수를 작성할 때 가위, 바위, 보 각각의 경우에서 이기는 경우로 나누어서 함수를 구현했다  
- 이 경우 같은 모양의 함수를 3개 만들어야하고,  코드가 길기 때문에 성능이 떨어진다는 단점이 있다   
(괜히 짧게 코드를 작성하기 위해 가독성을 해치는 것보단 이런식으로 누가봐도 알 수 있도록 코드를 작성하는 것이 좋을수도 있다)  


```swift
func compareWhenScissors() { // 가위일때
    switch playerSign {
    case .paper:
        print("졌습니다!")
    case .rock:
        print("이겼습니다!")
    case .scissors:
        print("비겼습니다!")
    }
}

 func compareWhenRock() { // 바위일떄
    switch playerSign {
    case .paper:
        print("이겼습니다!")
    case .rock:
        print("비겼습니다!")
    case .scissors:
        print("졌습니다!")
    }
}

 func compareWhenPaper() { // 보일때 
    switch playerSign {
    case .paper:
        print("비겼습니다!")
    case .rock:
        print("졌습니다!")
    case .scissors:
        print("이겼습니다!")
    }
}
```


<br>

#### 해결방법
스위치문 + where 조합으로 승패를 판단하는 함수를 만들어줬다  
```swift
func judgeWinner() {
    switch playerSign {
    case .rock where computerSign == .scissors:
        gameTurn = .player
        
    case .scissors where computerSign == .paper:
        gameTurn = .player
        
    case .paper where computerSign == .rock:
        gameTurn = .player
        
    case computerSign:
        gameTurn = .none
        
    default:
        gameTurn = .computer
    }
}
```

- 앞으로 이런 문제가 생기면  
- `다른사람이 이해하기 어려워도 성능을 챙겨야 함` vs `코드가 길더라도 남들이 이해하는게 중요함`  
- 둘 중에서 더 중요한게 뭔지 고민해볼것 같다

<br> 

## 브랜치 전략

