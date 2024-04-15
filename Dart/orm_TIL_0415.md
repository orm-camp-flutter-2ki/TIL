240415(Mon)

플러터 과정 25일차

## Remind Memo

freezed packege를 설치 할때 확인해야 할 것
=
pub.dev에 들어가서 freezed 검색해서 들어간 뒤에 installing 가서 설치하지 말고
Readme 탭에서 쭉 내려가서 How to use에 있는 Install에서 설치 할 것

#### 한번에 설치 할수 있는 코드

------------------------------------------------------------------------
```dart
flutter pub add freezed_annotation
flutter pub add dev:build_runner
flutter pub add dev:freezed
# if using freezed to generate fromJson/toJson, also add:
flutter pub add json_annotation
flutter pub add dev:json_serializable
```

#### GridView.count
사용시에 비율 정하는 법 childAspectRation를 사용하면 1 대 2, 1대 3 비율로 가로 세로 비율을 설정할 수 있다.
