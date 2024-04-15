240412 (Fri)

플러터 과정 24일차

메모


![image](https://github.com/BAUu/TIL/assets/44741680/967c5a07-aac8-462b-90a5-7e86425b2f2d)

뷰모델 로직 흐름

- UI 를 설명하는 속성이다
- UI 상태의 2가지 유형
  + Screen UI state
     - UI를 표시하기 위한 데이터들 (ViewModel 의 변수들)
  + UI element state
    - Widget 들의 상태를 관리하는 요소들 (TextEditingController 등)

![image](https://github.com/BAUu/TIL/assets/44741680/0f69ae9f-d4a2-495f-b274-6dbffeffc61c)

로직 UI는 정적인 속성이 아니다. (변수)
시간이 흐름에 따라 사용자 액션에 따라 변경되며 그 로직은 ViewModel이 담당한다.

### 로직의 종류

| ui  수명주기와 무관 | ui 수명 주기에 종속 |
| --- | --- |
| 비즈니스 로직 viewmodel 메서드 | ui로직 widget 내부의 로직 |
| 화면 ui 상태 viewmodel 변수 |  |

#### UI 상태 홀더의 책임
+ 간단한 UI
+ 유지 관리
+ 테스트 가능성
+ 가독
