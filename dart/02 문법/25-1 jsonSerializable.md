# jsonSerializable

## setting
### 1. IDE terminal
```dart
dart pub add json_annotation dev:build_runner dev:json_serializable
```
- pubspec.yaml 에서 확인 가능
<br/>

### 2. 
<div align="center">
<img width="264" alt="image" src="https://github.com/yujiyeong/TIL/assets/149862753/10dcea63-aeaa-4581-b9e6-8fe886d3fadb">
</div>

- Android -> setting

<div align="center">
<img width="1094" alt="image" src="https://github.com/yujiyeong/TIL/assets/149862753/d087c6e0-2ac4-4b54-9e1f-0ba2eae7e898">
</div>

- Live Templates -> Dart 선택

<div align="center">
<img width="125" alt="image" src="https://github.com/yujiyeong/TIL/assets/149862753/7a1363ae-d057-4d0f-acaf-30a2d883c26f">
<img width="216" alt="image" src="https://github.com/yujiyeong/TIL/assets/149862753/4687c08f-77df-43a2-9e67-5cc951e4d0d8">
</div>

- `+`  버튼 클릭 -> 1. Live Template 선택

<div align="center">
<img width="1094" alt="스크린샷 2024-04-01 오전 8 22 19" src="https://github.com/yujiyeong/TIL/assets/149862753/a7962122-143e-4a89-8d59-81716f5d93cc">
<img width="738" alt="스크린샷 2024-04-01 오전 8 22 23" src="https://github.com/yujiyeong/TIL/assets/149862753/3f3e5c40-8ef3-40f2-9b23-900d80d201ac">
</div>

- 아래 코드를 Template text: 에 복사 붙여넣기
- 세팅 따라한 후 `Apply`

```dart
import 'package:json_annotation/json_annotation.dart';

part '$NAME$.g.dart';

@JsonSerializable(explicitToJson: true)
class $CAP_NAME$ {
  $END$
  
  $CAP_NAME$();
  
  factory $CAP_NAME$.fromJson(Map<String, dynamic> json) => _$$$CAP_NAME$FromJson(json);
  
  Map<String, dynamic> toJson() => _$$$CAP_NAME$ToJson(this);
}
```

