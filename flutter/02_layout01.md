## Layout

StatefulWidget
- 단축키 : stful
- 상태를 가지는 위젯, 주로 화면에 변경사항을 있으면 다시 그려야하는 경우에 사용
- build() 메서드에서 화면을 그려야 함
- 이 외에도 initState(), dispose() 등의 생명주기 함수가 별도로 존재함

StatelessWidget
- 단축키 : stless
- 상태가 없는 위젯, 정적인 화면을 나타낼 때 사용
- build() 메서드를 오버라이드하여 화면을 그려야 함

MaterialApp
- Android 스타일로 개발할 때 최상위 위젯으로 설정해야 함
- iOS 스타일은 CupertinoApp

이미지 쓰는 법
- Asset을 pubspec.yaml 에 선언하고 이미지파일 로드
- <a href="https://docs.flutter.dev/ui/assets/assets-and-images">플러터 페이지 참조</a>
```dart
//pubspec.yaml
flutter:
  assets:
    - assets/my_icon.png
    - assets/background.png

//사진을 쓸 곳
return const Image(image: AssetImage('assets/background.png'));
```
