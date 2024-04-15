go router와 provider를 결합사용시
기존 provider를 사용할때

```dart
 home: ChangeNotifierProvider(   // cnp
        create: (_) => SearchListViewModel(
            subwayRepository: SubwayRepositoryImpl(
                subWayDataSource: SubWayDataSource()
            )
        ),
        child: const SearchMain(),
```

위와 같이 기존  runapp 함수에 의해 실행되는 클래스안에 home에 관련 provider코드가 들어가나

go router 사용시에  go router 안에서 앱의 시작화면 즉  initialLocation 설정에 해당하는 화면에 해당 

provider 관련 로직을 넣어 주어서 아래 예시처럼 사용하면 go router와 provider를 결합하여 정상적으로 사용할 수 있음을 확인

```dart
initialLocation: '/home',
  debugLogDiagnostics: true,
  routes: [
    GoRoute(
      path: '/home',
      builder: (context, state) {
        return ChangeNotifierProvider(
          create: (_) => SearchListViewModel(
              subwayRepository: SubwayRepositoryImpl(
                  subWayDataSource: SubWayDataSource()
              )
          ),
            child: const SearchMain(),
        );
      },
    )
```
