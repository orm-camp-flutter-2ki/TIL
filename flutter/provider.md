# Provider

[InheritedWidget](https://api.flutter.dev/flutter/widgets/InheritedWidget-class.html)을 더 쉽게 사용하고 보다 재사용할 수 있도록 만들어진 래퍼다.

[InheritedWidget](https://api.flutter.dev/flutter/widgets/InheritedWidget-class.html)을 직접 작성하는 것 대신 `provider`를 사용함으로써, 아래와 같은 이점을 가질 수 있다.

- 리소스의 단순화된 할당/해제
- 지연 로딩(lazy-loading)
- 클래스를 새로 만들 때 마다 매번 작성해야했던 부분을 크게 줄임
- devtool 친화적 : Provider를 사용하면 Application State가 Flutter devtool에 표시됨
- 이러한 [InheritedWidget](https://api.flutter.dev/flutter/widgets/InheritedWidget-class.html)들을 소비(consume)하는 일반적인 방법을 제시
- 복잡성이 기하급수적으로 증가하는 수신 매커니즘(listening mechanism)을 가진 클래스에 대한 확장성 향상

## 새로운 객체 인스턴스 노출하기

### 좋은 예

```dart
Provider(
  create: (_) => MyModel(),
  child: ...
)
```

### 안좋은 예

```dart
ChangeNotifierProvider.value(
  value: MyModel(),
  child: ...
)
```

```dart
int count;

Provider(
  create: (_) => MyModel(count),
  child: ...
)
```

안좋은 예와같이 생성했다면, 생성된 객체는 값이 변화해도 업데이트가 되지 않으므로 주의한다.

만약 시간에 따라 변경될 수 있는 변수를 객체에 전달하고 싶으면 ProxyProvider를 사용한다.

```dart
int count;

ProxyProvider0(
  update: (_, __) => MyModel(count),
  child: ...
)
```

## 기존 객체 인스턴스 재사용하기

기존 객체 인스턴스를 재사용하는 경우에는 반대로 .value생성자를 사용하는것이 좋다. 그렇지 않으면 객체가 아직 사용되고 있는 도중에 dispose가 호출될 수 있다.

### 좋은 예

```dart
MyChangeNotifier variable;

ChangeNotifierProvider.value(
  value: variable,
  child: ...
)
```

이미 존재하는 ChangeNotifier를 공급하기 위해서 .value를 사용한다.

### 나쁜 예

```dart
MyChangeNotifier variable;

ChangeNotifierProvider(
  create: (_) => variable,
  child: ...
)
```

ChangeNotifier의 기본 생성자를 사용해서 재사용하면 안된다.

## 값 읽기

값을 읽는 방법 3가지

1. watch : T의 변화를 지속적으로 관찰한다.
2. read: 단발성으로 T를 읽어온다.
3. select<T, R>T의 일부분 R을 읽어온다.

# 상태 모으기

ViewModel에 상태가 많아지면 UI 상태 홀더 클래스를 만들어 묶을 수 있다.

```dart
@freezed
class SearchListState with _$SearchListState {
  const factory SearchListState({
    @Default([]) List<Photo> photos,
    @Default(false) bool isLoading,
  }) = _SearchListState;
  factory SearchListState.fromJson(Map<String, Object?> json) => _$SearchListStateFromJson(json);
}
```

모델 클래스 만들듯(물론 다른 라이브 템플릿을 파야됨) freezed로 UI 상태 클래스를 만들고, 상태를 모은다. 여기서 required를 써도 되지만 @Default를 쓰서 기본값을 주는게 좋아보인다(?)

```dart
class SearchListViewModel with ChangeNotifier {
  final PhotoRepository _photoRepository;

  SearchListState _state = const SearchListState();
  SearchListState get state => _state;
}
```

이런 느낌으로 정리된다. 

```dart
void onSearch(String query) async {
  _state = state.copyWith(isLoading: true);
  notifyListeners();
  _state = state.copyWith(
    photos: await _photoRepository.getPhotos(query),
    isLoading: false,
  );
  notifyListeners();
}
```

상태 변경은 copyWith를 활용하면 끝.

정리

- 화면 하나에 하나의 UI 상태 홀더를 가지도록 한다
- 일반적으로 ViewModel 에서 처리한다
- 상태 홀더가 반드시 필요한 것은 아니다. 간단한 UI 는 간단히 처리하자
- ViewModel은 전체 화면에서만 사용해야 한다
- ViewModel의 인스턴스를 하위 UI 요소에 전파하지 않는다
