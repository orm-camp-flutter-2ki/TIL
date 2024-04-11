## 전종현의 TIL
하루동안 공부하며 정리한 내용을 업로드합니다.  
잘못된 내용이나, 오탈자가 있으면 언제든 알려주세요 :)

<br>

# Dart
[Dart.dev](https://dart.dev/guides) 공식문서를 읽고 학습하며 제 언어로 번역한 결과를 정리하였습니다.  
기본적으로 공식문서 + α의 내용을 담고 있지만, 중요도가 너무 낮은 내용은 생략하였습니다.

### Syntax basics
- [Variables](/Dart/Syntax%20basics/Variables.md)
- [Operators](/Dart/Syntax%20basics/Operators.md)
- [Comments](/Dart/Syntax%20basics/Comments.md)
- [Libraries & imports](/Dart/Syntax%20basics/Libraries&imports.md)

### Types
- [Built-in-types](/Dart/Types/Built-in%20types.md)
- [Records](/Dart/Types/Records.md)
- [Collection](/Dart/Types/Collection.md)
- [Generics](/Dart/Types/Generics.md)
- [Typedefs](/Dart/Types/Typedefs.md)
- [Type system](/Dart/Types/Type%20system.md)
- [Error handling](/Dart/Error%20handling)

### Concurrency
- [Concurrency in Dart](/Dart/Concurrency/Concurrency%20in%20Dart.md)
- [Asynchrony support](/Dart/Concurrency/Asynchrony%20support.md)

<br>

# Flutter
[api.flutter.dev](https://api.flutter.dev/), [docs.flutter.dev](https://docs.flutter.dev/) 공식문서를 읽고 학습하며 제 언어로 번역하였습니다.

## Flutter Api
- [BoxConstraints](/Flutter/Flutter%20Api/BoxConstraints.md)
- [BoxDecoration](/Flutter/Flutter%20Api/BoxDecoration.md)
- [BoxPainter](/Flutter/Flutter%20Api/BoxPainter.md)
- [BuildContext](/Flutter/Flutter%20Api/BuildContext.md)
- [Builder](/Flutter/Flutter%20Api/Builder.md)
- [Center](/Flutter/Flutter%20Api/Center.md)
- [ChangeNotifier](/Flutter/Flutter%20Api/ChangeNotifier.md)
- [Container](/Flutter/Flutter%20Api/Container.md)
- [Decoration](/Flutter/Flutter%20Api/Decoration.md)
- [InheritedWidget](/Flutter/Flutter%20Api/InheritedWidget.md)
- [LayoutBuilder](/Flutter/Flutter%20Api/LayoutBuilder.md)
- [Listenable](/Flutter/Flutter%20Api/Listenable.md)
- [ListenableBuilder](/Flutter/Flutter%20Api/ListenableBuilder)
- [Offset](/Flutter/Flutter%20Api/Offset.md)
- [Placeholder](/Flutter/Flutter%20Api/Placeholder.md)
- [Rect](/Flutter/Flutter%20Api/Rect.md)
- [SizedBox](/Flutter/Flutter%20Api/SizedBox.md)
- [State](/Flutter/Flutter%20Api/State.md)
- [StatefulBuilder](/Flutter/Flutter%20Api/StatefulBuilder.md)
- [ValueNotifier](/Flutter/Flutter%20Api/ValueNotifier.md)

## Flutter Docs
### Flutter Concepts
- [Understanding constraints](/Flutter/Flutter%20Docs/Flutter%20concepts/Understanding%20constraints.md)

## 기타 정리 문서
- [Provider](/Flutter/기타/Provider.md)

<br>

# Dev
기타 개발 관련 학습 내용 정리

### 편집 필요
- Typedefs의 `inline function types` -> `Effective Dart`
- Concurrency in Dart/Asynchrony support의 Futures, Streams, and async-await 파일로 연결
- Understanding constraints Flex, Listview 연결

### 정리 필요
- Key
- 3가지 tree
- RenderBox
- RenderObject
- FittedBox
- ConstrainedBox
- FractionallySizedBox
- AspectRatio
- MediaQuery
- MediaQueryData
- LayoutBuilder
- Flutter concept: https://docs.flutter.dev/resources/architectural-overview#hosting-flutter-content-in-a-parent-app