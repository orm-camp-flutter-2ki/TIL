## Result 패턴
> sealed class를 활용한 어떤 행동에 대한 상태 관리가 가능하다.

+ 네트워크 통신이나 데이터 처리 등의 로직에서 결과의 종류를 제한한다.
+ 예로 성공, 실패 시 처리방식을 따로 구현하여 각각 다른 결과를 도출시킨다.
+ 도출된 결과로 플러터에서 UI를 유연하게 컨트롤할 수 있고 Result 패턴을 쓰게되면 가독성 또한 높아진다.

## API사용법

+ 홈페이지에 API 카테고리에 들어가면 대부분 알 수 있다.
+ 홈페이지에서 제공하는 기능들에 대한 사용법?들이 친절히 설명되어있다.
+ 매개변수를 어떤걸 전달해줘야 하는지 확인하고 쿼리스트링으로 전달해주면 된다.
+ 실제로 임의의 매개변수를 전달한 결과값이 어떻게 뜨는지 Postman에서 확인할 수 있었다.

## Live Templates

+ 일정 패턴을 자동생성해주는 매우 고마운 기능이다.

+ Setting -> Edit -> Live Templates -> Dart 에 들어가서 + 눌러서 새로 생성.
+ Template text 부분에 자동 생성 코드를 입력.
+ 언어도 Dart로 변경하고 자동생성 키와 내용도 적어서 apply하면 끝

```dart
import 'package:freezed_annotation/freezed_annotation.dart';

part 'image_model.freezed.dart';

part 'image_model.g.dart';

@freezed
class ImageModel with _$ImageModel {
  const factory ImageModel({
    required String tags,
    required String previewURL,
  }) = _ImageModel;

  factory ImageModel.fromJson(Map<String, Object?> json) => _$ImageModelFromJson(json);
}
```
+ 빈칸에 적절한 이름을 적고 터미널에 dart run build_runner build --delete-conflicting-outputs를 실행하면 완성

## freezed
> freezed는 코드 생성 도구이며 불변 데이터 모델을 생성하는 데 사용된다.

+ 주로 값 객체나 데이터 전송 객체 등과 같은 불변 데이터 모델을 생성하는 데 사용된다.
+ 불변 데이터 모델은 객체가 생성된 후에 상태를 변경할 수 없는 객체를 의미하며 이는 데이터의 안정성과 예측 가능성을 높여준다.
+ 데이터 모델을 생성하는 데 매우 유용한 도구이며 코드의 반복 작성을 줄이고 유지보수성을 높여준다.

## 기타
오늘 imageApi 문제 풀면서 Result 패턴을 처음 쓰게 되었는데, Result의 success에도 toString을 재정의 해줘야 데이터가 제대로 뜨는것을 처음알았다.
오늘도 하나 배웠다.
