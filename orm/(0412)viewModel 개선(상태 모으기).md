## UI State(UI 상태)
* UI를 설명하는 속성이다.
* UI 상태의 2가지 유형
  * Screen UI state
    * UI를 표시하기 위한 데이터들(viewModel의 변수들)
  * UI element state
    * widget들의 상태를 관리하는 요소들(TextEditingController 등)

<p align="center"><img width="889" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/57e6dbd1-f02e-4f40-a045-154c08fab803"></p>

* UI 상태는 시간의 흐름에 따라, 사용자 액션에 따라 변경되는 변수이다.(정적인 속성이 아님)
* 그 로직은 viewModel이 담당한다.
* 로직의 종류

|UI 수명 주기와 무관|UI 수명 주기에 종속|
|---------------|---------------|
|비지니스 로직(= ViewModel 메서드)|UI 로직(= Widget 내부의 로직)|
|화면 UI 상태(= ViewModel 변수)||

#### => 수명 주기와 무관한 메서드와 변수는 viewModel로 따로 빼서 작성한다.

<br></br>

### UI 레이어의 로직 적용 흐름
<img width="579" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/629bf386-f20b-4980-bd95-4bb37b6cd472">

<img width="590" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/47bcc8e6-4db7-4c64-9341-a255b4e2f446">

=> 이것들이 모두 상태이다.  
=> UI 상태 홀더(UI 표현을 위한 상태를 저장하는 클래스)를 만들어 정리하자  
=> 별도의 클래스로 분리함으로써 코드의 중복을 줄이고 유지보수를 쉽게 할 수 있다.  
=> 상태 홀더 클래스를 사용하면 위젯의 상태 관리 로직을 위젯 자체에서 분리할 수 있다.(의존성 분리)  
=> 이를 통해 위젯은 UI에만 집중할 수 있고, 상태 관리는 별도의 클래스에서 처리된다.  
=> 단위 테스트하기 쉽다.  
=> 복잡한 UI 상태를 효율적으로 관리하고 변경사항을 추적하여 UI를 업데이트함으로써 앱의 성능을 향상시키고 사용자 경험을 향상시킨다.  

<br></br>

### UI 상태 클래스 만들기
1. freezed state 클래스를 만들고 여기에 상태 관리할 값들을 모은다.(data class가 되는 것)
📝 [선생님의 Live Template](https://gravel-pike-705.notion.site/Flutter-Live-Templeate-579bac3070754bdf8fa10afe4ebe8c92)

<img width="783" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/3d14ac18-abdd-4318-9367-aa289ff269e7">

<br></br>

2. ViewModel에 state 클래스를 임포트하고 state의 getter를 만든다.
<img width="470" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/6902fc69-18c8-4ce3-9b03-b102c7308100">

<br></br>

3. 기존에 있던 상태들의 getter 프로퍼티들은 없애도 된다.
4. viewModel에서 copyWith()을 활용해 변경사항만 안전하게 수정한다.
<img width="732" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/4b30fe68-3446-44b5-a9fc-49d25328b051">

<br></br>

5. view에서 UI 구현 시 state만 보면 된다.
<img width="731" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/73ce229d-7d44-4efb-9835-b3dd4e2b1ff0">

<br></br>

## 정리
* 화면 하나에 하나의 UI 상태 홀더를 가지도록 한다.
* 일반적으로 viewModel에서 처리한다.
* 상태 홀더가 반드시 필요한 것은 아니다. 간단한 UI는 간단히 처리하자
* viewModel에만 변수가 유지되게 하자.
* viewModel은 전체 화면에서만 사용해야 한다.
#### viewModel의 인스턴스를 하위 UI 요소에 전파하지 않는다.
  * => UI 재사용성이 떨어진다.
  * => 테스트 불가
  * => 디버깅이 어렵다.
#### 뷰가 아닌 공통 위젯들은 값만 받고 콜백으로 값을 던져야 유지 보수, 테스트를 할 수 있다.(뷰모델을 생성자에 직접 넣지 않는다.)
[참고: 선생님의 00_layout의 info_card 코드 참고](https://github.com/orm-camp-flutter-2ki/learn_flutter_together/blob/master/lib/00_layout/component/info_card.dart)  
<img width="407" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/7fdebaba-5fde-41fa-8225-1e9a89b605ec">
