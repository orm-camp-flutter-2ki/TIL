## StatefulWidget Lifecycle
<img width="600" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/e2a6fe39-0fb8-4a45-8047-fc98b9ca72dc">

#### [위젯 구축]
* createState()
  * statefulWidget()을 구축하자마자 호출된다.
  * 위젯 트리에 `상태`를 만든다.
  * 이 메서드는 반드시 존재해야 한다.
  * mounted is true
  * createState가 state 클래스를 생성하고 buildContext가 state에 할당된다.
  * BuildContext는 위젯이 배치된 위젯 트리의 위치를 단순화 한 것으로 모든 위젯은 bool 타입의 this.mounted 속성을 가지고 있다.
  * BuildeContext가 할당되면 true를 반환한다.
  * 위젯이 unmounted 상태일 때 setState()를 호출하면 에러가 발생한다.
* initState()
  * 위젯 트리 초기화
  * 화면 생성 때 단 한 번 호출된다.
  * 데이터 초기화 등을 실행할 수 있다.
* didChangeDependcies()
  * state 객체의 종속성이 변경될 때 호출된다.

#### [재드로잉]
* build()
  * 위젯으로 만든 UI를 구축한다.
  * 필수 구현이고 @override(재정의) 대상이다. 반드시 Widget을 반환해야 한다.
  * 변경된 부분 트리를 감지하고 대체한다. => 다양한 곳에서 반복적으로 호출된다.
* setState()
  * 상태가 변경되었을 때 프레임워크에 상태가 변경됨을 알린다.
* didUpdateWidget()
  * 위젯의 구성이 변경될 때마다 호출된다.
  * 부모 위젯이 변경되고 다시 그려져야 할 때 호출된다.
  * oldWidget 인수를 취득해 비교한다.

#### [Hot reload]
* ressemble() -> build()

#### [위젯 파기]
* deactivate()
  * state가 트리로부터 삭제될 때마다 호출된다.
* dispose()
  * 객체가 트리에서 완전히 삭제될 때 호출된다.
  * mounted is false

<br></br>

## FutureBuilder
#### future 를 사용한다면, 들어와야 하는 값이 최소 2개 이상(데이터가 없을 때, 있을 때, 로딩 중일때)이기 때문에 stateful 로 사용

```dart
FutureBuilder<String>(future: future 함수 작성, builder: (){
 }
)

builder 패턴: 어떤 데이터를 내가 원하는 형태로 만드는 패턴
```

<br></br>

## Navigation
#### Named Route 안 씀
#### 라우터 사용 (중규모 이상의 프로젝트에서 필수)
<img width="241" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/271375e3-dff4-40bf-a967-8b3a4fbcbce8">

* go_router에서 .go 는 웹에서 사용한다.(스택 교체=화면 완저 교체)
* 앱에서는 push만 사용하면 됨(스택에 쌓임)

<img width="519" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/aec4e94c-c153-4dde-9e98-f6433c8deafb">

* extra에 객체를 두 개 이상 전달하고 싶으면, 리스트로 보낸다. 받을 때 타입을 캐스팅해서 받는다.(as List<Todo>)
<img width="462" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/b4e440e4-7df8-4437-9265-5daec5299296">

<br></br>

## 기타
#### 피그마의 이미지를 그대로 복붙하여 사용할 수 있는지?
=> 개발자 용으로 코드등을 따로 만들어 주는 기능이 현재는 유료화되었다.
=> 그래도 간격이나 에셋 정도는 따로 다운이 가능하다.(export)

#### 라이브 템플릿 작성 방법
* 플러터 위젯용은 플러터에 적용한다.
* 커서가 들어갈 부분에 앞 뒤로 `$`를 붙인다. 예시 => Text('$title$')
* 커서를 이동하게 하고 싶으면 edit에서 설정 할 수 있다.
* 같은 이름(변수)로 등록하면 동시에 작성 가능하다.
* .jar 파일로 템플릿을 저장하면 다른 컴퓨터에서 해당 파일을 import에서 저장 및 사용 가능하다.

#### stateless 생성자에서 const를 빼면 재사용하지 않는다.
* final 필드가 있고 const를 사용하려면 외부에서 값을 받게 한다.
* 빌드 메서드 내부의 위젯 중 const가 아닌 건 계속 생성된다.(예시 :futureBuilder는 stateful 위젯)

<img width="200" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/6867ecff-40b8-4b37-89b0-8a55cf1dedfd">
<img width="200" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/50dab125-db70-4ea1-9352-a50b96a94bc4">

<img width="200" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/3e0520b7-8843-4fec-bb04-ac6e048e2257">
<img width="200" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/c3347961-aef7-4e17-8bcf-fd41a0899ab0">
