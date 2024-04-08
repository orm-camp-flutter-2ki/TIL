## Flutter Widget LifeCycle

Flutter에는 두 가지 유형의 위젯이 있다.

- Stateless Widgets
- Stateful Widgets

#### Stateless Widgets
- Stateless Widgets의 경우 생성자가 호출될 때만 빌드 함수(위젯을 빌드하는 역할)가 트리거된다.
  일단 생성되면 상위에서 업데이트 하지 않는 한 업데이트할 수 없다. 즉, 변경이 불가능하다. <br/>

#### Stateful Widgets
- Stateful Widgets의 경우 생성자가 호출되고 initState(), setState()가 호출될 때 빌드 함수가 트리거된다.
- Stateful Widgets은 내부적으로 state를 보유할 수 있으므로 상태가 변경될 때마다, 그리고 상위 항목이 변경될 때마다 업데이트될 수 있다. 수명 동안 여러 번 그릴 수 있다.

동적 위젯이 필요할 때는 Stateful 위젯을, 정적 위젯이 필요할 때는 Stateless 위젯을 선택한다. 가능한 스테이트풀 위젯의 사용을 제한하는 것이 좋다.

#### 생명주기 메서드의 종류

```

createState()

initState()

didChangeDependencies()

build()

didUpdateWidget()

setState()

deactivate()

dispose()
```

- `createState()`: 이 메서드는 위젯의 state를 생성한다. Stateful Widgets을 만들 때 프레임워크에서 createState() 메서드를 호출하므로 변경하고 싶을 때에는 이 메서드를 재정의해야 한다.

![image](https://github.com/Gunbam27/TIL/assets/95085649/976ef1bb-787a-4696-89f2-0b91a157f05d)

- `initState()`: 이 메서드는 state 개체가 생성된 후 호출되며 위젯의 상태를 초기화하는 데 사용된다.

- `didChangeDependencies()`: 이 메서드는 initState 바로 뒤에 호출되며, 상속된 위젯을 통해 state 개체의 종속성이 변경될 때 호출된다.

- `build()`: 이 메서드는 상태 개체가 초기화된 후에 호출된다. 위젯 트리를 구축하는 데 사용되며 initState, dDChangeDependencies, dDUpdateWidget 또는 setState 호출을 통해 상태가 변경될 때마다 호출된다.

- `didUpdateWidget()`: 이 메서드는 위젯이 새 속성으로 업데이트될 때 호출된다. 일반적인 경우는 부모가 생성자를 통해 자식() 위젯에 일부 변수를 전달하는 경우이다.

- `setState()`: setState() 함수 안에서의 호출은 state 에서 무언가 변경된 사항이 있음을 Flutter Framework 에 알려주는 역할이다. 이로 인해 UI 에 변경된 값이 반영될 수 있도록 build 메소드가 다시 실행된다.

- `deactivate()`: 프레임워크는 트리에서 이 State 개체를 제거할 때마다 이 메서드를 호출한다. 그리고 하위 트리에서 GlobalKey를 사용하여 다시 삽입될 때 호출된다. 이로 인해 프레임워크가 dispose 메서드를 호출할 때까지 대부분의 리소스 해제를 연기할 수 있다.(무슨말인지...)
  
- `dispose()`: 이 메서드는 위젯이 영구적으로 파괴될 때 호출된다. 이 메서드는 네트워크 연결을 닫거나 애니메이션을 중지하는 등 위젯에서 사용하는 리소스를 해제하는 데 사용된다.


#### 참고문서
https://medium.com/gytworkz/flutter-widget-lifecycle-everything-you-need-to-know-629d01ca4a09

