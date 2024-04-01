# freezed
[[🔗 freezed dev 문서]](https://pub.dev/packages/freezed)   
- live template 등록 방법은 앞전에 jsonSerializable과 동일하다. [🔗link](https://github.com/yujiyeong/TIL/blob/main/dart/02%20%EB%AC%B8%EB%B2%95/25-1%20jsonSerializable.md)
- 조금이라도 수정 시, 빨간 줄이 없더라도 `build`를 **꼭** 다시 해주어야 한다.

## file nesting
- 나중에 많아질 `.g.dart` `.freezed.dart` 파일들을 1분도 안걸려 토글처럼 접어주는 기능을 추가할 수 있다.  
### search
<div align="center">
<img width="700" alt="image" src="https://github.com/yujiyeong/TIL/assets/149862753/bf04bb62-fa3c-43e8-98dc-b2299d479180">
</div>

- `shift` 3번 연타
- `File nesting` 선택

### edit
<div align="center">
<img width="479" alt="image" src="https://github.com/yujiyeong/TIL/assets/149862753/1856d8c7-a3bf-43fc-b160-2a137cbdffff">
</div>

```
.g.dart; .freezed.dart;
```

- `.dart`에 해당하는 칸, 오른쪽 제일 끝에 위의 text를 붙여 넣고 `ok` 눌러주면 끝  
<br/>

## setting
```dart
dart pub add freezed_annotation
dart pub add dev:build_runner
dart pub add dev:freezed
```
- pubspec.yaml 파일에 추가
<br/>

```dart
// fromJson(), toJson()
dart pub add json_annotation
dart pub add dev:json_serializable
```
- 위 명령어를 통해 fromJson(), toJson() 도 추가할 수 있다.
- `jsonSerializable`단계를 통해 이미 추가했었다면 해주지 않아도 괜찮다.  
<br/>

```dart
dart run build_runner build  (watch)
dart run build_runner build --delete-conflicting-outputs (충돌 해결)
```
- build 명령어도 똑같다.
- 아래 코드 (충동 해결)로 build 하는게 낫다. 이 방법들을 통해 만들어진 파일들은 찌꺼기가 남기 때문에, 삭제하는 등의 충돌이 있으면 `build`가 안되기 때문에 피패해진다고 한다.  
<br/>


## data class
### Live Template 추가
- 아래 코드를 Template text: 에 복사 붙여넣기
```dart
import 'package:freezed_annotation/freezed_annotation.dart';

part '$NAME$.freezed.dart';

part '$NAME$.g.dart';

@freezed
class $CAP_NAME$ with _$$$CAP_NAME$ {
  const factory $CAP_NAME$({
    $END$
  }) = _$CAP_NAME$;
  
  factory $CAP_NAME$.fromJson(Map<String, Object?> json) => _$$$CAP_NAME$FromJson(json); 
}
```
<br/>

## 사용 방법
### 작성
<div align="center">
<img width="700" alt="스크린샷 2024-04-02 오전 1 03 30" src="https://github.com/yujiyeong/TIL/assets/149862753/5c43538c-bd2f-4b38-8aa4-536937fd64c4">
<img width="612" alt="스크린샷 2024-04-02 오전 1 01 08" src="https://github.com/yujiyeong/TIL/assets/149862753/e25f638d-c7a4-4775-ba6c-020d501c2cec">
<img width="700" alt="스크린샷 2024-04-02 오전 1 01 18" src="https://github.com/yujiyeong/TIL/assets/149862753/3925dc8e-b664-4110-b720-bec467947650">
</div>

- 등록했던 `Abbreviation` 으로 사용 가능
- 경로가 맞는지 확인, 파일 이름과 클래스 이름이 같은지 확인  

### build
<div align="center">
<img width="700" alt="스크린샷 2024-04-02 오전 1 01 46" src="https://github.com/yujiyeong/TIL/assets/149862753/8e583ddb-c6f7-4a2c-83c4-9be1ba2f5cd4">
<img width="700" alt="image" src="https://github.com/yujiyeong/TIL/assets/149862753/32cb7129-07c2-4c17-a480-c26d881b485a">
<img width="700" alt="image" src="https://github.com/yujiyeong/TIL/assets/149862753/9b552146-5577-406d-8677-161f6f15d598">
</div>

- `JsonSerializable`과 다른 점이 있다면, 채워 주어야하는 것이 `field`가 아니라 `constructor` 라는 것이다.
- model class 만들 듯이 타입 명시와 함께 `required` 키워드를 꼭 붙여주어야 한다.
- IDE 터미널에 `build` 명령어 실행, 전에 사용했던 명령어는 키보드 방향키 `↑`로 이동할 수 있다.
- 그러면 토글처럼 접혀진 상태로 생성되어 있다. 수정 시 `build` 명령어 다시 실행하기
<br/>

## sealed
### Live Template 추가
- 아래 코드를 Template text: 에 복사 붙여넣기
```dart
// dart 3.0 이후
import 'package:freezed_annotation/freezed_annotation.dart';

part '$NAME$.freezed.dart';

@freezed
sealed class $CAP_NAME$<T> with _$$$CAP_NAME$<T> {
  const factory $CAP_NAME$.success(T data) = Success;
  const factory $CAP_NAME$.error(String e) = Error;
}
```
<br/>

## 사용 방법
### 작성
<div align="center">
<img width="700" alt="스크린샷 2024-04-02 오전 1 20 32" src="https://github.com/yujiyeong/TIL/assets/149862753/ed6baf69-df17-4f2e-ac85-35189f4217c6">
<img width="612" alt="스크린샷 2024-04-02 오전 1 20 34" src="https://github.com/yujiyeong/TIL/assets/149862753/3dadf1f7-21ef-43e3-b6ea-08e74bbd567e">
<img width="700" alt="스크린샷 2024-04-02 오전 1 20 52" src="https://github.com/yujiyeong/TIL/assets/149862753/45cb4904-f466-4f91-b58d-ed848353308e">
</div>

- 등록했던 `Abbreviation` 으로 사용 가능
- 경로가 맞는지 확인, 파일 이름과 클래스 이름이 같은지 확인  

<br/>

### build
<div align="center">
<img width="700" alt="스크린샷 2024-04-02 오전 1 21 18" src="https://github.com/yujiyeong/TIL/assets/149862753/e8185b9c-9b8a-4847-bdc7-4de4cd3d7bc6">
<img width="700" alt="스크린샷 2024-04-02 오전 1 21 43" src="https://github.com/yujiyeong/TIL/assets/149862753/a1d3f93d-0e4f-4627-ba7b-10ece88f590e">
</div>

- IDE 터미널에 `build` 명령어 실행, 전에 사용했던 명령어는 키보드 방향키 `↑`로 이동할 수 있다.
- 그러면 토글처럼 접혀진 상태로 생성되어 있다. 수정 시 `build` 명령어 다시 실행하기
<br/>

## Freezed 활용
### sealed - Result Pattern
- 기본적으로 예외는 try - catch 를 활용하여 처리하지만, 런타임 에러 뿐만 아니라 논리적인 오류나 예외 상황에 대한 처리를 하기에는 부족  
- Result 클래스는 성공 시에는 `데이터`를, 실패 시에는 `Exception`(또는 String)을 담는 객체를 정의, 이 외의 반환 케이스가 필요하면 추가하면 된다.  
- sealed 클래스는 타입 봉인 효과를 가진다, `enum` 하고 비슷한 효과 + 다른 객체의 참조를 가질 수 있다는 것  
[[🔗 sealed dev 문서]](https://dart.dev/language/class-modifiers#sealed)   

### Result class
- 범용적으로 사용하기 때문에 class name을 특정적으로 짓지 말고 `Result`로 가는 것이 좋다.
- api 파일보다는 repository를 구현하는 파일에서 사용하는 것이 추후 관리가 편하다.
<br/>

### 기본 버전 : Exception 만 처리  
```dart
import 'package:freezed_annotation/freezed_annotation.dart';

part 'result.freezed.dart';

@freezed
sealed class Result<T> with _$Result<T> {
  const factory Result.success(T data) = Success;
  const factory Result.error(String e) = Error;
}
```
<br/>

### 신 버전 : 원하는 에러 타입 정의 가능
`D` : 데이터  
`E` : 에러  
```dart
import 'package:freezed_annotation/freezed_annotation.dart';

part 'result.freezed.dart';

@freezed
sealed class Result<D, E> with _$Result<T> {
  const factory Result.success(T data) = Success;
  const factory Result.error(String e) = Error;
}
```
<br/>

#### 선언  
```dart
  @override
  Future<Result<List<Photo>>> getPhoto(String query) async {
    try {
      final photos = await _api.getPhotosApi(query);
      if(query == '바보') return Result.error('비속어를 사용할 수 없습니다');
      return Result.success(photos.map((e) => e.toPhotos()).toList());
    } catch (error) {
      return Result.error('알 수 없는 네트워크 에러');
    }
  }
```
```dart
// 성공 시 List<Todo> 리턴, 실패 시 String 에러메시지를 리턴
Future<Result<List<Photo>, String>> getPhoto(String query) {}

// 성공 시 Todo 리턴, 실패 시 Exception 객체를 리턴
Future<Result<Photo>, Exception> getPhoto(String query) {}
```
<br/>

#### 호출  
```dart
void main() async {
  final PhotoRepository photo = PhotoRepositoryImpl(PhotoApiImpl());
  final result = await photo.getPhoto('yellow+flowers');

  switch (result) {
    case Success<List<Photo>>():
      print(result.data);
    case Error<List<Photo>>():
      print(result.error);
  }
}
```
<br/>
