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

## FutureBuilder



## 기타
#### 피그마의 이미지를 그대로 복붙하여 사용할 수 있는지?
=> 개발자 용으로 코드등을 따로 만들어 주는 기능이 현재는 유료화되었다.
=> 그래도 간격이나 에셋 정도는 따로 다운이 가능하다.(export)

#### 라이브 템플릿 작성 방법
* 플러터 위젯용은 플러터에 적용한다.
* 커서가 들어가고
