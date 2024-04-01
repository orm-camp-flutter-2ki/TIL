>🙋🏻왜 사용해? <br>
일반적으로 성공 또는 실패와 같은 두 가지 결과를 표현하여 안정성을 높이기 위해서!<br>
Result 패턴은 여러가지 종류의 성공과 실패를 처리하기 용이한 패턴이다<br>
앱의 규모에 맞는 Result 패턴을 사용하자<br>
소규모 기본유형 으로 충분 -> freeze 사용 가능<br>
다국어 지원 : 제네릭 2가지 버전<br>

>🙋🏻sealed class?<br>
sealed class 는 서브타입을 봉인한다<br>
sealed class 는 패턴매칭을 활용하여 모든 서브타입에 대한 처리를 하기 용이하다<br>


> **기본유형**<br>
```dart 
sealed class Result<T> {
 factory Result.success(T data) = Success;
 factory Result.error(Exception e) = Error;
}
class Success<T> implements Result<T> {
 final T data;
 Success(this.data);
}
class Error<T> implements Result<T> {
 final Exception e;
 Error(this.e);
}
```

>** 제네릭 2가지 선언**
(성공과 실패시 데이터값을 정확히 볼수 있다!)
```dart
sealed class Result<T, E> {
   factory Result.success(T data) = Success<T, E>;
   factory Result.error(E error) = Error<T, E>;
 }
 class Success<T, E> implements Result<T, E> {
  final T data;
  Success(this.data);
 }
class Error<T, E> implements Result<T, E> {
  final E error;
  Error(this.error);
 }
 ```
 
 > @freeze 사용
 (기본유형 자동입력 버전)
 ```dart
 import 'package:freezed_annotation/freezed_annotation.dart';
part 'result.freezed.dart';
@freezed
sealed class Result<T> with _$Result<T> {
  const factory Result.success(T data) = Success;
  const factory Result.error(String e) = Error;
}
```

패턴 사용하는 곳 : <br>
Result 패턴을 도입하는 곳에서 응답 객체를 Result 클래스로 랩핑하기<br>
> 기본구성 일 경우
```dart
abstract interface class PhotoRepository {
  Future<Result<List<Photo>>> getPhotos(String q);
}
```
```dart
class PhotoRepositoryImpl implements PhotoRepository {
  final PhotoApi _api = PhotoApi();
  @override
  Future<Result<List<Photo>>> getPhotos(String q) async {
    if (q == '바보') {
      return Result.error(('비속어를 사용할 수 없습니다.'));
    }
    //  예외가 예상되는 지점에서 try - catch 사용하기
    try {
      final hitsDtoList = await _api.getPhotos(q);
      // HitsDto를 Photo로 변환
      final photoList =
          hitsDtoList.map((hitsDto) => hitsDto.toPhoto()).toList();
      return Result.success(photoList);
    } catch (e) {
      return Result.error(('알 수 없는 네트워크 에러: $e'));
    }
  }
}
```
> 제네릭 2가지 선언<br>
```dart
sealed class Result<T, E> {
  factory Result.success(T data) = Success<T, E>;
  factory Result.error(E error) = Error<T, E>;
}
```
``` dart
final PhotoApi _api = PhotoApi();
  @override
  // Future<Result<List<Photo>, Exception>> 타입 잘 확인할것!
  Future<Result<List<Photo>, Exception>>  getPhotos(String q) async {
    if (q == '바보') {
      return Result.error(Exception('비속어를 사용할 수 없습니다.'));
    }
    try {
      final hitsDtoList = await _api.getPhotos(q);
class PhotoRepositoryImpl implements PhotoRepository {
          hitsDtoList.map((hitsDto) => hitsDto.toPhoto()).toList();
      return Result.success(photoList);
    } catch (e) {
      return Result.error(Exception('알 수 없는 네트워크 에러: $e'));
    }
  }
}
```


> TEST CODE
```dart 
 final repository = PhotoRepositoryImpl();
  test('test 바보', () async {
    // freezd 사용할 시에만 사용 가능!
    // .whenOrNull(error: (e) => e) String type 변환하는 기능
    final expected = '비속어를 사용할 수 없습니다.';
    final repository = PhotoRepositoryImpl();
    final result = await repository.getPhotos('바보');
    final error = result.whenOrNull(error: (e) => e);
    expect(error, expected);
  });
 swich 사용해서 강제로 모든 케이스 실행
  test('test yellow', () async {
    final result = await repository.getPhotos('yellow');
    switch (result) {
      case Success<List<Photo>>():
        print('성공 : ${result.data}');
      case Error<List<Photo>>():
        print('실패 : ${result.e}');
    }
  });
  ```
  
  >**Result 패턴 사용시 효과**<br>
 [ enum ](https://velog.io/@hee462/Dart-enum)과 동일하게 switch 문과 조합하여 모든 처리를 강제할 수 있다<br>
여러가지 3개 이상의 성공과 실패를 처리할 있다<br>
sealed랑 헷갈려하는데 간단히 설명하면<br>
enum값은 클래스의 인스턴스이며, 고정된 값(상수값을 그룹화)<br>
sealed class는 클래스가 상속될 수 있는 하위 클래스의 종류를 명시적으로 제한 -> 그렇기때문에 swich문 default 선언 안함<br>


 
