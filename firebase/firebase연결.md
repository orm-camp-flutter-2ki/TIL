firebase console

https://console.firebase.google.com/

1. 프로젝트 생성
2. 작업공간 준비
flutter sdk설치
firebase cli 설치 및 로그인(firebase login)
3. flutter project create
4. dart pub global activate flutterfire_cli
5. flutterfire configure --project=flutter-git-blog-abb08
firebase console에서 정한 이름은 flutter-git-blog까진데, abb08까지 더 붙음
플랫폼정함
firebase_options.dart 생성됨

6. firebase 초기 및 플러그인 추가
flutter pub add firebase_core
```dart
import 'package:firebase_core/firebase_core.dart';

  
import 'firebase_options.dart';

  
// ...main에 추가
await Firebase.initializeApp(    options: DefaultFirebaseOptions.currentPlatform,

  
);
```