## iOS 커리어 스타터 캠프

# 묵찌빠 프로젝트 저장소

## 목차
- [Flow Chart](#플로우-차트)
- [코딩 컨벤션](#코딩-컨벤션)
- [커밋 컨벤션](#커밋-컨벤션)
- [그라운드 룰](#그라운드-룰)

## 플로우 차트

![](https://github.com/ICS-Asan/ios-rock-paper-scissors/blob/step1/FlowChart.png)
- step1
  - 게임 문구 출력
  - 컴퓨터의 패 할당
  - 사용자 입력
  - 입력값 판단
    1) 잘못된 입력
    2) 게임 종료
    3) 게임 승패
  - 입력값 판단 결과 출력(입력 오류, 게임 결과, 종료)

## 코딩 컨벤션
- https://github.com/StyleShare/swift-style-guide (스타일쉐어 코딩 컨벤션 참고)
- 들여쓰기는 xcode default로 사용
- 부호 앞뒤로 띄우기
- return타입이 있는 경우 함수내에서 줄바꿈(나머지는 줄바꿈X)
- 타입은 명시!
- 함수 하나는 5~7줄(최대한 맞춰보기!)

## 커밋 컨벤션
- 커밋 제목
  - subject와 body 사이는 한 줄 띄워 구분하기
  - subject line의 글자수는 50자 이내로 제한하기
  - subject line의 첫 글자는 대문자 사용하기
  - subject line의 마지막에 마침표(.) 사용하지 않기
  - subject line에는 명령형 어조를 사용하기
feat = 주로 사용자에게 새로운 기능이 추가되는 경우
fix = 사용자가 사용하는 부분에서 bug가 수정되는 경우
docs = 문서에 변경 사항이 있는 경우
style = 세미콜론을 까먹어서 추가하는 것 같이 형식적인 부분을 다루는 경우 (코드의 변화가 생산적인 것이 아닌 경우)
refactor = production code를 수정하는 경우 (변수의 네이밍을 수정하는 경우)
chore = 별로 중요하지 않은 일을 수정하는 경우 (코드의 변화가 생산적인 것이 아닌 경우)

- 커밋 단위: 함수 생성 및 변경사항 발생 시
- 커밋은 한글로 작성

## 그라운드 룰
- 시간
  - 스크럼시간: 총 2회(아침: 9시 30분, 저녁: 11시 40분), 매 20분
  - 마치는 시간: 12시
- 커뮤니케이션
  - 이해가 가지 않는 것, 모르는 것 등 넘어가지 않고 바로바로 피드백
  - 지금의 컨디션에 대해 숨기지 않기
  - 거짓말하지 않기
- 스크럼 내용
  - 전날 구현한 기능이 무엇인지(어려웠던 점, 배운점)
  - 전날 학습한 내용을 바탕으로 어떻게 적용해 볼지
  - 본인의 컨디션
  - 아침에 설정한 것들을 얼마나 잘 수행했는지(저녁 스크럼)
