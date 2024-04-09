# inheritedWidget
[[🔗 공식 유튜브 총 정리]](https://www.youtube.com/watch?v=og-vJqLzg2c)

- 원하는 위젯으로 원하는 객체를 의존성 주입(Dependency Injection)을 해 주는 위젯
    - 의존성 주입용 위젯
</br>

## 왜 사용하나?

[[🔗 참고 블로그]](https://lucky516.tistory.com/124)

<div align="center">
<img width="666" alt="image" src="https://github.com/yujiyeong/TIL/assets/149862753/2137469b-66ef-487c-865c-f45084430484">
</div>

- 가장 하위의 붉은색 widget이 root state에 데이터를 필요로 하는 경우, 중간 과정의 모든 widget의 생성자에 state 데이터를 뚫어줘야 한다.
- 어떤 객체가 다른 객체에서 사용되도록 하기 위해서는 생성자를 통해 필요한 객체를 전달하는 것이 일반적이다. 다만 생성자를 통한 의존성 주입은 의존성 트리가 깊어질수록 단계를 많이 타야한다.
- 코드가 지저분해진다
- InheritedWidget은 이런 단점 해소를 위해 나온 것
</br>

## inheritedWidget
<div align="center">
<img width="666" alt="image" src="https://github.com/yujiyeong/TIL/assets/149862753/1b05c618-29e2-4035-95f2-10d74ef25824">
</div>

- 최상단에 InheritedWidget을 놓고 데이터를 저장하면 하위 트리에서 공유자원으로 사용, 하위 widget들은 이를 어디서든지 바로 접근이 가능하다
    - ex) 쇼핑 어플의 장바구니, 어디서든 접근 가능해야 함
- 루트 중간에 두면 잔가지에게만 전달되고, 다른 가지에는 관련이 없어서 전달이 안된다.
    - 다른 가지와도 공유하려면? 더 상위로 옮긴다.
    - 전체가 공유하려면 `main`의 `MyApp()`까지 올려서 꽂아준다.
- page 전환 시 공유하려면 코드가 지저분해지고 의존성이 생긴다...
    - `go_route` 사용하는게 좋다. `go_route` 를 사용하면 InheritedWidget의 코드를 숨겨준다.
- 생성자로 통하지 않고 위젯 트리 아래에서 바로 꽂아버리는…
    - ex) MediaQuery, Theme 와 같이 어디서나 사용하고 싶을 때
</br>

## of() 와 buildContext
[[🔗 참고 블로그]](https://lucky516.tistory.com/122?category=1065021)
### buildContext

> `context` 란?
*A handle to the location of a widget in the widget tree.*
현재 Widget의 Widget tree 상의 위치에 관한 정보를 담고있는 변수라는 뜻이다.
> 
- Widget tree에 접근하려면 반드시 BuildContext의 `context` 가 필요
</br>

### .of(context)

- 하위 widget에서 InheritedWidget에 접근하려면 .of(context) 메서드를 이용하면 된다.
- Widget tree 에 접근하려면 반드시 BuildContext `context` 가 필요하다
- `dependOnInheritedWidgetOfExactType` : Widget tree에서 현재 Widget의 위쪽 방향으로 가장 가까운 타입을 찾는 메서드
    
    > *ex) Mycolor.of(context).color*
    > 
    > 
    > 현재 context 기준에서 Widget tree 위쪽 방향으로 가장 가까운 Mycolor의 color를 찾는 것
    > 
- `bool updateShouldNotify` : 수정되었는지 알려주는 규칙을 정의하는 메서드
    - (`covariant InheritedWidget`) : override 후 parameter type 수정을 허용하는 것
    - `build` 가 필요한 경우 true, 필요 없는 경우 false를 리턴하도록 하자
    - 무분별한 rebuild를 컨트롤할 수 있다
    - 이전 데이터(old Widget)을 새 데이터와 비교할 수 있다.
    - **주의 할 점** : `initState()` 에서 하면 안되고 `didChangeDependencies()` 에서 해야한다.
    - 왜냐면 `initState()`는 context 까지 접근을 못한다.

<div align="center">
<img width="666" alt="image" src="https://github.com/yujiyeong/TIL/assets/149862753/600d1516-4ed5-45c7-9e6f-5b84f3c7c6bd">
</div>

- 전달하고자 하는 InheritedWidget을 최상위와 중간에 다시 배치했을 경우엔?
    - Widget tree 위쪽 방향에서 현재 `context` 와 가장 가까운 타입을 찾는다. 위 경우 Data2
</br>

### 주의할 점

> *ex) Mycolor.of(context).color*
> 
> 
> 현재 context 기준에서 Widget tree 위쪽 방향으로 가장 가까운 Mycolor의 color를 찾는 것
> 
- 위 코드를 예시로 들면
- 내 context 기준으로 가장 가까운 Mycolor를 찾으려 하는데 기준이 되는 BuildContext 위로 더이상의 Mycolor가 없을 때 에러가 난다
- 이럴 경우 Builder 함수를 통해 중간을 끊고, 새로운 context를 만들어주면 해결 가능하다
</br>

## 바로 꽂아버리는 위젯들 예시

- MediaQuery.of(context).size
    - 화면에 대한 여러가지 정보를 가지고 있음
    - 어떤 화면에서도 사용할 수 있음
    - widget을 MediaQuery에 연동하고, MediaQuery가 변동할 때마다 rebuild
- Theme
- 상태 관리
    - flutter_bloc
    - Provider
    - 인기 있는 상태 관리 솔루션도 동일한 메커니즘이다.
</br>

## BuildContext

- `BuildContext`
- 위젯 트리 정보를 알고 있는 객체 (신)
- 이거 없으면 화면 이동, 다이얼로그가 실행 안 됨
- 관심이 있는 대상을 위해 Widget tree를 검색할 때 사용
</br>

## flutter의 주요 tree 3가지

- Widget Tree
- Element Tree
- RenderObject Tree
</br>
