---
title: State
author: Kim Donghyeok
created_at: 2024-04-07
updated_at: 2024-04-07
tags:
  - 생존코딩
  - 오름캠프
  - flutter
reference: https://api.flutter.dev/flutter/widgets/State-class.html https://medium.com/@hadiyaaamir222/lifecycle-of-a-stateful-widget-aece2d56c946
---

# State

> [[StatefulWidget]] 을 위한 내부 상태 또는 로직

State 는 다음과 같은 정보이다.

1. 위젯이 빌드될 때 동기적으로 읽을 수 있는 정보
2. 위젯의 life cycle 동안 변경 될 수 있는 정보

State 객체는 [[StatefulWidget]] 이 확장되어 tree에 삽입될 때, 프레임워크에 의해 StatefulWidget.createState 메소드를 호출하여 생성된다. 주어진 StatefulWidget 이 여러번 확장 될 수 있기 때문에 주어진 StatefulWidget 인스턴스와 연관된 두 개 이상의 State 객체가 존재 할 수 있다. 마찬가지로 StatefulWidget 이 tree에서 삭제 될 때나 나중에 tree에 삽입 될 때도 프레임워크는 createState 를 호출하여 새로운 State 객체를 생성해  State 객체의 생명주기를 단순화한다.

State 객체는 다음과 같은 생명 주기를 가진다.

- 프레임워크는 StatefulWidget.createState 메소드를 호출하여 State 객체를 생성한다.
- 새롭게 생성된 State 객체는 [[BuildContext]] 와 연관된다. 이러한 연관성은 영구하다 : State 객체는 자신의 BuildContext를 절대로 변경하지 않는다. 하지만, BuildContext 자신은 tree 와 그 subtree 주위로 이동이 가능하다. 이 시점에서 State 객체를 mount 된 것으로 간주 된다.
- 프레임워크가 [[initState]] 를 호출한다. State 의 자식클래스는 initState 메소드가 호출될 때, 각각 context 나 widget의 속성으로 사용가능 할 수 있는 BuildContext 나 위젯에 연관되어 일회성 초기화를 수행하기 위해 initState 메소드를 반드시 재정의 해야한다.  
- 프레임워크는  [[didChangeDependencies]] 메소드를 호출한다. State 의 자식 클래스는 [[InheritedWidget]] 과 연관된 초기화를 하기 위해 didChangeDependencies 를 재정의 해야한다.  만약 [[BuildContext.dependOnInheritedWidgetOfExactType]] 이 호출되었을 때, 상속된 위젯이 이후에 변경되거나 위젯이 트리에서 이동하는 경우, didChangeDependencies 메소드는  다시 호출 된다.
- 이 시점에서 State 객체는 완전히 초기화 되고 프레임워크는 이 하위트리의  사용자 인터페이스에 대한 묘사를 얻기 위해 해당 [[build]] 메서드를 여러번 호출 할 수 있다. State 객체는 자신의 setState 메소드를 호출하여서 자발적으로  그 subtree 대한 rebuild 를 요청할 수 있다. 이는 내부 상태의 일부가  변경되어 사용자 인터페이스의 subtree 에 영향을 줄 수 있음을 나타낸다.
- 이 시간 동안, 상위위젯은 동일한 runtimeType 과 WIdget.key 를 가진 새로운 위젯을 화면에 표시하기 위해 tree update 에서 이 위치를 rebuild 하고 request 할 수 있다. 이 작업이 일어 날 때, 프레임워크는 새 위젯을 참조하도록 widget 속성을 업데이트하고 이전 위젯을 인자로 가지는 [[didUpdateWidget]] 메소드를 호출한다. State 객체는 연관된 위젯의 변화에 응답하기 위해  didUpdateWidget 를 재정의해야 한다. (예. 암시적으로 에니메이션을 시작하기 위해) 프레임워크는 항상 didUpdateWidget. 메소드가 호출된 후 buiild 메소드를 호출한다. 이는 didUpdateWidget 안의 setState 메소드의 모든 호출은 중복이라는 뜻이다.
- 개발 중에, 만약 hot reload 가 발생 한다면. [[ressemble]] 메소드가 호출된다. 이것은 initState 메소드에서 준비 된 모든 데이터를 다시 초기화 시킨다.
- 만약, State 객체를 가진 하위 tree 가 tree 에서 제거된다면 (예를들어, 상위 트리가 다른 runtimeType 과 Widget.key 를 가진 위젯을 만들어서) 프레임워크는 [[deactivate]] 메소드를 호출한다. 하위클래스는 tree 의 이 객체와 연결된 다른 element 를 clean up 하기 위해 반드시 이 메소드를 재정의해야한다.
- 이 시점에서 프레임워크는 tree 다른 부분에 이 하위 tree 를 다시 삽입한다. 이 작업이 일어난다면 프레임워크는 State 객체가 tree 의 새로운 위치에 적응하기 위해 하위트리의  build 메소드를 호출하는 것을 보장해야 한다. 만약, 프레임워크가  이 하위 tree를 다시 삽입하는 경우 , 그 작업은 트리에서 제거된 하위트리의 애니메이션 프레임이 끝나기 전에 수행된다. 이러한 이유로, State 객체는  프레임워크가 dispose 메소드를 호출하기 전까지  대부분의 리소스 해제를 연기할 수 있다.
- 만약 프레임워크가 현재 애니메이션 프레임이 종료 될 때까지 하위트리를 다시 삽입하지 않으면, 프레임워크는 [[dispose]] 메소드를 호출한다. 이는 State 객체가 다시 빌드 되지 않음을  의미한다. 하위 클래스는 이 메소드를 재정의 하여 이 객체가 보유한 리소스를 해제해야 한다.
- 프레임워크가 dispose 를 호출한 후 State 객체는 unmounted 된 것으로 간주하고 mount 속성은 false 가 된다. 이 시점에서 setState 를 호출하는 것은 에러이다. 이 단계는 생명주기에서 최종단계이다. 삭제된 State 객체를 다시 mount 할 수 없다.

# 정리

1. `createState()` : StatefulWidget 이 생성 될 때 그 생성자가 호출되고 위젯을 초기화 한다. createState() 메소드가 실행 되고 위젯에 State 객체를 생성한다.
2. `initState()` : 위젯이 위젯 트리에 삽입된 후, 객체가 처음 생성될 때 호출된다.
3. `didChangeDependencies()` : 위젯의 종속성이 변경 될 때 호출된다. 위젝이 일부 외부 데이터에 의존하거나 상위 위젯에서 데이터를 상속 받을 때 유용하다.`initState()` 이후에도 호출된다.
4. `build()` : 현재 상태를 기반으로 위젯의 사용자 인터페이스를 빌드한다. 이 메소드는 위젯이 위젯 트리에 처음 삽입 될 때 처음에 호출되며, 위젯을 다시 빌드 해야 할 때 수명주기 동안 반복적으로 호출 될 수 있다.
5. `setState()` : 상태가 변경되고 관련 메소드가 다시 호출 되면 위젯 rebuild 를 트리거 한다.
6. `didUpdateWidget()` : 업데이트 된 속성으로 위젯이 다시 빌드 될 때 트리거 된다. build() 다음으로 호출 되며 이전 위젯 속성과 현재 위젯 속성을 비교할 수 있다.
7. `deactivate()` : 위젯이 트리에서 제거되었지만 다시 삽입 될 수 있을 때 호출 된다.
8. `dispose()` : 위젯이 위젯 트리에서 영구적으로 제거될 때 호출되어 위젯이 보유한 리소스를 해제한다.
9. `ressemble()` 핫 리로드 중에 앱이 재 어셈블 될때 호출 된다.

![[240407_state_life_cycle.png]]
