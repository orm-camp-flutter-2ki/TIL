## inheritedWidget

- 원하는 위젯으로 원하는 객체를 의존성 주입(Dependency Injection)을 해 주는 위젯
- 의존성 주입용 위젯

## 왜 필요한가?
- 변화가 필요한 위젯이 필요한 데이터를 받기 위해서는 트리의 Top 에서 Bottom 까지 생성자를 통한 데이터 전달이 필요하다.
  
[예시] Screen안에 impl안에 Api....뚫고 뚫고 뚫고
![image](https://github.com/Gunbam27/TIL/assets/95085649/3129fd88-045f-4fe8-9a9c-b30094139779)

## 그래서 생성자 없이 의존성 주입 하려면?


### .of(context)
- 하위 widget에서 InheritedWidget에 접근하려면 .of(context) 메서드를 이용하면 된다.
- Widget tree 에 접근하려면 반드시 BuildContext context 가 필요하다.
- 최상단에 InheritedWidget을 놓고 데이터를 저장하면 하위 트리에서 공유자원으로 사용, 하위 widget들은 이를 어디서든지 바로 접근이 가능하다
  ex) 쇼핑 어플의 장바구니, 어디서든 접근 가능해야 함
  즉, 전체가 공유하려면 main의 MyApp()까지 올려서 꽂아준다.

- 전달하고자 하는 InheritedWidget을 최상위와 중간에 다시 배치했을 경우엔?
  Widget tree 위쪽 방향에서 현재 context 와 가장 가까운 타입을 찾는다.

## inheritedWidget 예시
- MediaQuery.of(context).size : 기기 사이즈 정보
- Theme : 레이아웃 theme정보
- 상태관리 라이브러리 (flutter_bloc,Provider...등등)
인기 있는 상태 관리 솔루션도 동일한 메커니즘이다.
