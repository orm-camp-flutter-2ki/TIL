# icon.svg 
> 원하는 icon이 없을 경우 추가하는 방법 작정  
### 공식 페이지 링크
[[🔗 bev package_svg]](https://pub.dev/packages/flutter_svg)  

## install 명령어
- IDE 터미널에...
- `pubspec.yaml` 에서 확인... 
```
flutter pub add flutter_svg
```

## project에 `assets/icon` directory 만들기
- `assets directory`는 밖에 꺼내두는게 일반적인 것 같다.  
<div align="center">
  <img width="555" alt="image" src="https://github.com/yujiyeong/TIL/assets/149862753/7c806662-8138-46e1-8879-2e2d7ab3fe58"></div>

- 그렇지만 나는 layout에 넣어뒀었다... 다음부턴 밖에 꺼내야지....  
<div align="center">
  <img width="555" alt="image" src="https://github.com/yujiyeong/TIL/assets/149862753/6693e2ca-883d-4a76-a4d6-635c2f5004b4"></div>

## `icons`에 svg 이미지 추가하기
### 1. drag and drop
<div align="center">
  <img width="555" alt="image" src="https://github.com/yujiyeong/TIL/assets/149862753/25ea228f-0711-498b-b3ef-1565128acc0a"></div>

### 2. project 내 경로에 직접 추가
<div align="center">
  <img width="555" alt="image" src="https://github.com/yujiyeong/TIL/assets/149862753/9bcbd443-3f06-4d2c-a09f-3d614547bc48"></div>

## pubspec.yaml에서 asset 활성화
- 오타 혹은 띄어쓰기, 들여쓰기에 주의...  
<div align="center">
  <img width="555" alt="image" src="https://github.com/yujiyeong/TIL/assets/149862753/1ed563c8-b15e-494e-8c7a-1963741c3ca9"></div>

## 코드작성
<div align="center">
  <img width="555" alt="스크린샷 2024-04-04 오전 5 02 26" src="https://github.com/yujiyeong/TIL/assets/149862753/c942afeb-a7f7-4254-a5a7-df9e50270412"></div>

```dart
import 'package:flutter_svg/svg.dart';

  // (...)

SvgPicture.asset('assets/icons/instagram.svg', width: 18,)

  // (...)
```
- (, width: [원하는 크기],)
