# JsonSerializable

직렬화와 역직렬화를 간편하게 제작할 수 있게 도와주는 패키지인 json_serializable 패키지를 어떻게 활용할 수 있는지에 대해 알아보겠습니다.

https://pub.dev/packages/json_serializable
패키지 정보는 해당 링크에서 확인할 수 있습니다.

### 설치
json_serializable 뿐만 아니라 json_annotation과 build_runner가 사전에 설치되어 있어야 합니다.

json_annotation : https://pub.dev/packages/json_annotation
build_runner : https://pub.dev/packages/build_runner

이 세 가지를 한 번에 설치하고 싶다면 아래 명령어를 입력하면 됩니다.
```
dart pub add json_annotation dev:build_runner dev:json_serializable
또는
flutter pub add json_annotation dev:build_runner dev:json_serializable
```

pubspec.yaml 파일에 이 세 가지 패키지가 정상적으로 등록되었다면 성공입니다.

<br>

### 세팅

json_serializable 패키지를 사용하기 위해서는 아래와 같은 형식이 갖춰져있어야 합니다.

```dart
import 'package:json_annotation/json_annotation.dart';

part 'person.g.dart';

@JsonSerializable()
class Person {
  final String name;
  final int age;

  Person({
    required this.name,
    required this.age
  });

  factory Person.fromJson(Map<String, dynamic> json) => _$PersonFromJson(json);

  Map<String, dynamic> toJson() => _$PersonToJson(this);
}
```
fromJson과 toJson에서 빨간 줄이 뜨면서 컴파일 오류가 생기는 건 정상입니다.
여기서 위와 같이 세팅한 후에 명령어를 입력하면 person.g.dart에서
fromJson과 toJson이 구현됩니다.

<br>

### 적용
```
dart run build_runner build
또는
dart run build_runner build --delete-conflicting-outputs (충돌 해결)
```
해당 명령어를 콘솔에서 실행할 경우 part 키워드를 사용한 파일명으로 파일이 하나 생성됩니다.
생성된 파일의 형식은 아래와 같습니다.

```dart
// GENERATED CODE - DO NOT MODIFY BY HAND

part of 'person.dart';

// ***********************************
// JsonSerializableGenerator
// ***********************************

Person _$PersonFromJson(Map<String, dynamic> json) =>
    Person(
      name: json['name'] as String,
      age: json['age'] as int,
    );

Map<String, dynamic> _$PersonToJson(SpokenLanguage instance) =>
    <String, dynamic>{
      'name': instance.name,
      'age': instance.age,
    };
```
이렇게 fromJson과 toJson이 구현되었습니다.

이 외에 추가적인 유용한 기능으로 @JsonKey annotation을 이용하여 Json의 Key와 모델의 필드를 다르게 지정해줄 수도 있습니다.
```dart
import 'package:json_annotation/json_annotation.dart';

part 'person.g.dart';

@JsonSerializable()
class Person {
  final String name;
  @JsonKey(name: 'korean_age')
  // 자동으로 person.g.dart에서 age 필드와 korean_age 키를 맞춰줌
  final int age;

  Person({
    required this.name,
    required this.age
  });

  factory Person.fromJson(Map<String, dynamic> json) => _$PersonFromJson(json);

  Map<String, dynamic> toJson() => _$PersonToJson(this);
}
```
