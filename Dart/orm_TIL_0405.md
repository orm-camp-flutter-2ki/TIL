240405 (Fri)

플러터 과정 25일차

메모
![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/86296f50-858e-40b3-b09a-5faedc04c2f9/406ee63e-8c03-4b11-94e3-dafb57b75119/Untitled.png)

setState는 빌드를 다시 불러오는 것

그래서 안티 패턴이다.

이렇게 하면 무한으로 돈다.

위젯 빌드에서 로직을 수행해서는 안된다.

최악의 안티 패턴이다.

데이터를 언제 얻어야할까?

빌드 전에 해야 한다.

**void initState()**

initState 함수로 불러올 수 있다.

initState는 생성자 같은 느낌으로 처음 빌드를 할때만 실행되고 이후에는 실행 되지 않는다.

initState는 stateful일때만 사용 된다.

변수 사용이 있어서 휴먼에러 발생 가능성이 있다.

CircularProgressIndicator()

로딩중 표시: 원 빙글빙글 도는 거

## 네비게이션

새로운 화면으로 이동(navpush)

```dart
onPressed: () {
	Navigator.push(
		context,
		MaterialPageRoute(builder: (context) => const SecondRoute()),
		);
	}
```

원래 화면으로 돌아가기 (navpop)

```dart
onPressed: () {
	Navigator.pop(context);
	}
```
# StatefulWidget class

StatelessWidget class와 달리 변경 가능한 상태를 갖는 위젯이다.

상태는 위젯이 빌드될때 동시에 읽을 수 있고 

위젯 수명 동안 변경될 수 있는 정보

1. **createState()**: StatefulWidget가 생성될 때 호출되며, 상태 객체를 생성합니다.
                      이 메서드는 반드시 오버라이드되어야 합니다.
2. **initState()**: 상태 객체가 생성되고 위젯 트리에 추가된 후에 호출됩니다.
                    한 번만 호출되며, 일반적으로 초기화 작업이 여기서 수행됩니다.
3. **didChangeDependencies()**: 위젯이나 그 부모 위젯이 의존성에 변경이 있을 때 호출됩니다.
                                예를 들어, 위젯이 다른 위젯으로부터 데이터를 받아와야 하는 경우 이 메서드에서 데이터를 가져올 수 있습니다.
4. **build()**: 위젯의 UI를 빌드하고 반환하는 메서드입니다.
                 이 메서드는 반드시 오버라이드되어야 하며, Flutter 프레임워크가 호출하여 위젯의 UI를 렌더링합니다.
5. **didUpdateWidget(oldWidget)**: 위젯이 새로운 구성을 받아 업데이트되었을 때 호출됩니다.
                                   예를 들어, 부모 위젯이 재구성되어도 해당 위젯의 상태를 유지해야 할 때 사용됩니다.
6. **setState(fn)**: 위젯의 상태가 변경되었음을 프레임워크에 알리고, UI를 다시 렌더링할 수 있도록 하는 메서드입니다.
                     이 메서드를 호출하면 **`build()`** 메서드가 다시 호출되어 UI가 업데이트됩니다.
7. **dispose()**: StatefulWidget이 위젯 트리에서 제거되기 전에 호출됩니다.
                    여기서 리소스를 해제하거나, 이벤트 구독을 취소하는 등의 정리 작업을 수행할 수 있습니다.

위의 메서드들은 StatefulWidget의 생명주기 동안 호출되는 주요한 메서드들입니다.
이러한 메서드들을 사용하여 상태를 관리하고, UI를 업데이트하고, 리소스를 해제하는 등의 작업을 수행할 수 있습니다.
