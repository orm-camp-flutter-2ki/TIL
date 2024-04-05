**Future 를 UI로 표현하는 방법**

StatefulWidget + setState()

FutureBuilder

생산성을 위해서 라이브 템플릿을  만드는 것이 좋다. 

라이브 템플릿 백업하면 같은 기종 (windows,mac)만 해야 한다.

데이터 소스에서 데이터 가져올때  build에서 then메서드 안에서 setState안에서 

값을 갱신하는 경우 수많이 build수행된다 그래서 build 데이터 안에서 데이터 요청로직 절대 금지

대안으로 데이터 소스에서 가져온 데이터를 가져오는 로직을 initState를 수행한다  

데이터 소스를 가져오는 경우 로딩상태를 정의할 필요가있는데 여러 상태가  필요한 경우 함수를

이용하여서 작성한다. 

![Untitled 1](https://github.com/happysong3914/TIL/assets/130008915/7e3f49df-4283-4994-82e4-a94dd8b9fcb3)


FutureBuilder

- Future 함수의 결과를 Widget으로 변환하는 위젯
- snapshot 에 데이터와 에러 정보 등이 들어 있음

FutureBuilder에 

snapshot 객체에서 연결 상태를 알 수 있음 이걸 이용하여 연결 상태에 따라서  로직 분할할수 있다.

```dart
ConnectionState.none; 
ConnectionState.waiting;
ConnectionState.active;
ConnectionState.done; 
```

stateless라도 const 안붙이면 재사용 되지 않는다. → 메모리 낭비 막음

FutureBuilder 만들때 스트림빌더로 만들고 수정하면 편한장점

---

# **Navigation**

화면 전환을 말 함

다른 화면으로 전환 : push

다시 되돌아 오기 : pop

=> 화면 표시는 Stack 구조로 관리된다

push() 함수는 Future를 리턴하는 타입 nullable로 값을 받아야 한다.

고급 라우팅을 사용하려면 go_router 패키지를 사용한다. 특히 웹 지원하려면 무조건 사용한다.

[https://pub.dev/packages/go_router](https://pub.dev/packages/go_router)

앱 내부에서 인터넷 브라우저 처럼 주소값 처럼 관리 하기 위해서 사용하는데

GoRoute함수에서  path 파라미터에서 주소를 String로 명시적으로 작성하고

builder 파라미터에 주소와 매칭되는 화면의 위젯을 지정해준다.

또한 inital로케이션에 시작 화면 설정가능

화면이동 예시 

![Untitled](https://github.com/happysong3914/TIL/assets/130008915/80d62936-9209-4267-a65b-d56d1ad8fd95)


문서에는 push 대신 go로 나와있으나  push 만쓴다고 생각해라

RestFul 하게 화면 끼리 이동하면서 통신하기 위해서 

state 파라미터에 통신 관련 데이터들이 담겨져 있다.

toJson() 으로 직렬화 가능하다면 String 으로 변환하여 객체를 전달 가능

어떤 데이터라도 직렬화, 역직렬화를 통해 주고 받을 수 있음

직렬화 역직렬화 해서 queryParmeters 받는 이유는 String으로 보내고 받기 때문이다.

extra 방식으로  보낼때는 객체 하나만 주고 받을 수 있다 여러개 보내야 하면

리스트 객체에 여러 객체를 담아서 보낸다. 

Nested Route

라우터 내부에 라우터 구성 가능

- StatefulWidget 의 생명주기 조사

StatefulWidget  위젯의 생명 주기를 알아야 하는 이유는 위젯의 생명주기에 대한 이해를 통해 데이터의 전달 시점 화면종료 시 어떤 로직을 수행할지 결정 가능

**createState()**

StatefulWidget이 최초로 생성시 처음 createState() 메서드가 호출하고  StatefulWidget의 상태를 관리하는 State 객체를 생성함 생성 이유는  State 가 상태를 관리 하기 때문

**initState()**

State 객체가 초기화시 호출, 주로 일회성 작업수행 (초기데이터 로드나 컨트롤러 초기화)

**didChangeDependencies()**

상위 위젯 또는 InheritedWidget 등의 종속성이 변경시 didChangeDependencies() 메서드 호출

위젯이 생성될 때보다 많이 호출되는데, 이전에 의존성이 변경되었을 때 실행 즉 데이터를 가져오거나 업데이트시 활용

**build()**

위 단계 완료시  build() 메서드를 통해  화면 작성 , build() 는 상태변경시 화면을 다시그리기 위해 호출됨

**didUpdateWidget()**

상위 위젯이 재호출 되어  랜더링 되어 해당 StatefulWidget을 다시 작성 시 didUpdateWidget() 메서드가 호출

**setState()**

User의 조작으로  StatefulWidget의 상태 변경시 , setState() 메서드를 호출되어 상태 변경

**deactivate()**

StatefulWidget이 비활성시 deactivate() 메서드가 호출, 필요 정리작업 수행로직 수행

**dispose()**

StatefulWidget이 종료시, dispose() 메서드가 호출 , 메모리 누수 방지및  리소스를 해제 로직을 작성하여 메모리 누수 방지
