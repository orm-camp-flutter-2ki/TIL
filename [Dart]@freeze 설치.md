

> 🙋🏻?
freezed = json_serializable + Equatable + Immutable 합친 느낌
1. toJson / fromJson 함수를 제공해 json으로 쉽게 serialize / deserialize 할 수 있도록 돕는다. 
2. equals (==)와 hashCode를 자동으로 작성해준다.
3. 선언된 필드들의 getter를 만들어서 외부에서 값을 변경할 수 없도록 한다. 
4. copy와 copyWith을 자동으로 구현해주고, 종속성을 가지는 하위 클래스들에 대해서도 쉽게 deepCopy 할 수 있도록 도와준다.
5. sealed class 작성을 편하게 해 준다

```dart
flutter pub add freezed_annotation
flutter pub add dev:build_runner
flutter pub add dev:freezed
# if using freezed to generate fromJson/toJson, also add:
flutter pub add json_annotation
flutter pub add dev:json_serializable
```

``` dart
빌드명령어 : 오류나면 사용, 혹은 파일 매칭 안될때도
dart run build_runner build --delete-conflicting-outputs
```
> ⭐️ 관련자료 <br>
>[공식문서 freeze](https://pub.dev/packages/freezed)<br>
[data class 생성 ](https://gravel-pike-705.notion.site/Flutter-Live-Templeate-579bac3070754bdf8fa10afe4ebe8c92?pvs=4)<br>

