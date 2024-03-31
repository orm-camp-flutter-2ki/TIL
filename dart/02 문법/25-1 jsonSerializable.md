# jsonSerializable
## setting
### 1. IDE terminal
```dart
dart pub add json_annotation dev:build_runner dev:json_serializable
```
- `pubspec.yaml` 파일 에서 확인 가능
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
<br/>

## 사용 방법
### 1. json
<div align="center">
<img width="1153" alt="스크린샷 2024-04-01 오전 8 29 18" src="https://github.com/yujiyeong/TIL/assets/149862753/47a1e293-ba85-44aa-a6f7-6dbb7e90be0e">
<img width="612" alt="스크린샷 2024-04-01 오전 8 29 20" src="https://github.com/yujiyeong/TIL/assets/149862753/22ad6cd3-2bcf-4eba-93dd-120f472669d7">
<img width="1153" alt="스크린샷 2024-04-01 오전 8 29 35" src="https://github.com/yujiyeong/TIL/assets/149862753/6de16719-91d8-49d9-ba50-da11c19a7e8e">
</div>

- 등록했던 `Abbreviation` 으로 사용 가능

### 2. field & constructor 작성
> 참고 사항  
> 이 단계에서 field name은 표기법 + 모델클래스에서 사용할 name으로 작성

<div align="center">
<img width="1153" alt="스크린샷 2024-04-01 오전 8 46 47" src="https://github.com/yujiyeong/TIL/assets/149862753/22d33948-1faa-4bb9-b329-747efa065c20">
</div>

### 3. 활성화
<div align="center">
<img width="1153" alt="스크린샷 2024-04-01 오전 8 47 07" src="https://github.com/yujiyeong/TIL/assets/149862753/09d21cc6-78d7-4f82-898f-f41ac86a5886">
</div>

```dart
dart run build_runner build  (watch)
dart run build_runner build --delete-conflicting-outputs (충돌 해결)
```

- (watch) 의 코드라인을 `terminal` 에 입력해 활성화

### 4. JsonKey 어노테이션
<div align="center">
<img width="1153" alt="스크린샷 2024-04-01 오전 8 47 40" src="https://github.com/yujiyeong/TIL/assets/149862753/eb2a816f-67f1-466b-a5bc-d7e5b0002067">
<img width="1153" alt="스크린샷 2024-04-01 오전 8 47 57" src="https://github.com/yujiyeong/TIL/assets/149862753/665df6d2-7710-4d96-bd3a-1dca91af7e82">
</div>

```dart
  @JsonKey(name: 'first_name')
  final String firstName;

  @JsonKey(name: 'last_name')
  final String lastName;
```

- `JsonKey` 를 사용해 모델의 필드로 맵핑 가능  
- 생성된 `[파일명].g.dart`은 절대 건드리지 않는다!!!  










