_Go Dart_

# Result 패턴
##### 1 FUNC) 
##### - Result 클래스는 성공 시에는 데이터를, 실패 시에는 Exception(또는 String)을 담는 객체를 정의함.
##### 2 DIFFER) try-catch & Result pattern
> 기본적으로 예외는 try-catch 를 활용하여 처리.
> 그러나 try-catch의 경우, 다양한 에러(런타임 에러, 논리적인 오류나 예외 상황에 대한 처리)애 대처하기 어려움.
> Result 패턴을 활용한 대처.
> 서버에 데이터 요청시 예상되는 상황:
> - 성공 (Success) or 실패 (Error, Failure) *네트워크 연결 X 혹은 불안정으로 인한 타임아웃.

##### 3 CODE)
##### (1) sealed class 활용
##### - sealed 클래스는 타입 봉인 효과를 가짐. *enum과 비슷한 효과 + 다른 객체의 참조를 가질 수 있음
##### - Sample Code
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
##### (2 FUNC) 
##### - Result 패턴을 도입하는 곳에서 응답 객체를 Result 클래스로 랩핑하기

```dart
Future<List<Photo>> fetch(String query);
Future<Result<List<Photo>>> fetch(String query);
```

##### - enum 과 동일하게 switch 문과 조합하여 모든 처리를 강제할 수 있음.
##### - 클래스의 특성을 가진 enum같은 느낌임. *enum은 동등성 비교 및 해시 코드 재정의가 안됨.
##### - 여러가지 3개 이상의 성공과 실패를 처리할 수 있음.

```dart
final repository = UserRepository();

final usersResult = await repository getUsers);

switch (usersResult) {
  case Success<List<User>>:
    print('성공: ${usersResult.data.toString()}');
  case Error<List<User>>:
    print('실패: ${usersResult.message}');
```
##### (3) freezed 라이브러리
##### - freezed = json_serializable + Equatable + Immutable 합친 느낌
> 1. toJson / fromJson 함수를 제공해 json으로 쉽게 serialize / deserialize 할 수 있도록 돕는다. 
> 2. equals (==)와 hashCode를 자동으로 작성해준다.  
> 3. 선언된 필드들의 getter를 만들어서 외부에서 값을 변경할 수 없도록 한다. 
> 4. copy와 copyWith을 자동으로 구현해주고, 종속성을 가지는 하위 클래스들에 대해서도 쉽게 deepCopy 할 수 있도록 도와준다.  
> 5. sealed class 작성을 편하게 해 준다.

##### - 설치 방법
> Terminal
> dart pub add dev:build_runner  
> dart pub add dev:freezed  
> // fromJson(), toJson()  
> dart pub add json_annotation  
> dart pub add dev:json_serializable  

##### (4.1) (freezed를 활용한) Result 클래스 ver.1
```dart
import 'package:freezed_annotation/freezed_annotation.dart';

part 'result.freezed.dart';

@freezed
sealed class Result<T> with _$Result<T> {
  const factory Result.success(T data) = Success;

  const factory Result.error(String e) = Error;
}
```

##### (4.2) (freezed를 활용한) Result 클래스 ver.2
```dart
import 'package:freezed_annotation/freezed_annotation.dart';

part 'result.freezed.dart';

@freezed
sealed class Result<D, E> with _$Result<D, E> {
  const factory Result.success(D data) = Success;

  const factory Result.error(E error) = Error;
}
```
### freezed를 활용한 Data Class (모델) 작성
```dart
import 'package:freezed_annotation/freezed_annotation.dart';

part 'photo.freezed.dart';
part 'photo.g.dart';

@freezed
class Photo with _$Photo {
  const factory Photo({
    required String tags,
    required String imageUrl,
    @Default(false) bool isCompleted,
  }) = _Photo;

  factory Photo.fromJson(Map<String, Object?> json) => _$PhotoFromJson(json);
}
```
_PRACTICE 1._
