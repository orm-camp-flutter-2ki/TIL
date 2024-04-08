# StatefulWidget
- statefulWidget 안에서  setState()안에 로직을 정리하면 상태가 바뀝니다.
- statefulWidget 안에 상태를 만들어주고 관리하게끔 createState() 메서드를 만들어야 합니다.

# FutureBuilder
- FutureBuilder  비동기 작업의 결과를 기다리면서 화면을 업데이트하는 Flutter 위젯입니다.

# navigator
- 화면 이동을 위한 위젯입니다.
- 새로운 화면으로 이동 (navpush)
- 원래 화면으로 돌아가기 (navpop)

고급 라우팅을 사용하려면 go_router 패키지를 사용한다. 특히 웹 지원하려면 무조건 사용한다.

라우팅 테이블 : 계획
URL 경로 및 파라미터 : 목표
라우터 :  앱내에서 특정 동작을 통해 새로운 화면으로 이동하고자 할때 라우터는 해당경로에 맞는 화면을 찾아 표시합니다.
동적 라우팅 : 사용자의 입력이나 앱의 상태에 따라 동적으로 화면을 전환할 수 있습니다.

