> flutter pub add provider

provider 를 사용하기 위에 최 상단에 작성한다
```dart
ChangeNotifierProvider(
                create: (_) => SubWayViewModel(
                    repository: SubwayRepositoryImpl(
                  subwayApi: SubwayApi(),
                )),
                child: HomeScreen(),
```

```dart

  @override
  Widget build(BuildContext context) {
    final viewModel = context.watch<SubWayViewModel>();

    return Scaffold(
```
- context.watch<SubWayViewModel>()는 현재 위젯 트리에서 SubWayViewModel 타입의 인스턴스를 찾아 반환합니다. watch 메서드는 Provider의 변경 알림을 받아 SubWayViewModel이 변경될 때마다 HomeScreen 위젯을 다시 빌드
   
>- viewModel 변수를 사용하면 SubWayViewModel의 상태나 메서드를 사용할 수있다 만약 프로바이더를 사용하지 않았더라면?
```dart
    void _searchSubWay(String keyword) {
    viewModel.searchSubWay(keyword); // ViewModel의 메서드 호출
    setState(() {}); // 상태 변경을 반영하여 화면을 다시 그립니다.
  }
}
```  
  이런형식으로 작성되기때문에 상태관리와 ui업데이트 효율성이 떨어짐으로 provider를 사용해야한다!
  
