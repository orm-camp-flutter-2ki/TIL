# provider 
### 상태관리란 ? 
- 상태 관리(state management)는 앱의 상태(데이터)를 효율적으로 관리하고, 앱의 UI가 그 상태에 따라 적절히 반응하도록 하는 것을 의미합니다.
- 변수를 수정하면 알아서 UI도 바뀌게 하는것이 목표
- 여러가지 방법
  = setState() 
  = InheritedWidget + (ValueNotifier 또는 ChangeNotifier)
  = provider 라이브러리 사용 ( 구글에서 추천 )

### provider의 상태관리 구성
- ChangeNotifierProvider, ChangeNotifier 조합
- ChangeNotifierProvider ( 최상위 위젯에 위치, ChangeNotifier를 감시)
- notifyListeners() ( 변경을 통지 )

### provider의 사용법
- 관찰 대상 객체 작성 (ChangeNotifier)
- provider 의존성 추가 ( flutter pub add provider )
- ChangeNotifier를 제공할 부분에 ChangeNotifierProvider 위젯 배치
- watch() 는 지속적인 관찰을 하고 변경시 build() 를 리빌드 함. build() 메서드 내에서 사용
- 단발성 이벤트 처리 (read() 로 접근, read() 는 지속적인 관찰이 아닌 단발성 접근에 사용 : initState() 또는 버튼 클릭 등 )
- 룰
   - 다음 룰을 따를 것 
    - build() 에서는 watch
    - 단발성 실행은 read
    - initState() 에서는 Future.microtask() 후에 read
