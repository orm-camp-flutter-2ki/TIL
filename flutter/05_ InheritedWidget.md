### InheritedWidget

`InheritedWidget` class: 
- 데이터를 저장하고 자식 위젯에 전달하는 데 사용 ( 상태를 관리하는 역할 )

`of()`:
- 자식 위젯에서 InheritedWidget에 액세스하기 위한 메서드
- 이 메서드를 사용하여 InheritedWidget에서 저장된 데이터를 사용할 수 있음

`updateShouldNotify()` :
- InheritedWidget에서 데이터가 변경되었을 때 자식 위젯에게 알리는 데 사용
- 이를 통해 자식 위젯은 새 데이터를 사용하여 자체를 다시 그릴 수 있음

- InheritedWidget을 사용하면 많은 수의 하위 위젯에 동일한 데이터를 전달할 필요가 없으므로 코드를 효율적으로 유지할 수 있음
- InheritedWidget은 상태를 관리하기 위한 Provider 패키지와 함께 사용되는 경우가 많음 Provider는 InheritedWidget을 훨씬 더 쉽게 사용할 수 있도록 도와주는 패키지

`buildContext`

context 란?
- A handle to the location of a widget in the widget tree.
- 현재 Widget의 Widget tree 상의 위치에 관한 정보를 담고있는 변수라는 뜻

Widget tree에 접근하려면 반드시 BuildContext의 context 가 필요


### 주의할 점
ex) Mycolor.of(context).color

현재 context 기준에서 Widget tree 위쪽 방향으로 가장 가까운 Mycolor의 color를 찾는 것

위 코드를 예시로 들면
내 context 기준으로 가장 가까운 Mycolor를 찾으려 하는데 기준이 되는 BuildContext 위로 더이상의 Mycolor가 없을 때 에러가 난다
이럴 경우 Builder 함수를 통해 중간을 끊고, 새로운 context를 만들어주면 해결 가능하다

### BuildContext
BuildContext
위젯 트리 정보를 알고 있는 객체 (신)
이거 없으면 화면 이동, 다이얼로그가 실행 안 됨
관심이 있는 대상을 위해 Widget tree를 검색할 때 사용


---

출처. https://github.com/orm-camp-flutter-2ki/TIL/pull/704/files?short_path=42c6d6a#diff-42c6d6ae519be989bb13272dcc1b2278d24a57fe42cb47ed7b065d3f14d2abdb
