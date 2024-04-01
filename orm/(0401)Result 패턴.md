## Result
### 에러 처리
기본적으로 예외는 try - catch 를 활용하여 처리한다.  
하지만 런타임 에러뿐만 아니라 논리적인 오류나 예외 상황에 대한 처리를 하기에는 부족하다.  
✅ Result 패턴은 성공, 실패 시 처리에 유용한 패턴이다.

### 성공과 실패 중 하나를 리턴하는 Result 클래스 예시
* Result 클래스는 성공 시에는 데이터를, 실패 시에는 Exception(또는 String)을 담는 객체를 정의한다.
* 이 외에도 더 많은 반환 케이스가 필요하면 추가한다.
* sealed 클래스는 타입 봉인 효과를 가진다.(enum하고 비슷)

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

### 사용 예시
* 응답 객체를 Result 클래스로 랩핑하기
<img width="683" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/1543806d-966d-44ed-9feb-0964e01a92a8">

* 예외가 예상되는 지점에서 try - catch 사용하기
<img width="481" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/9b458b04-b0c0-4ce1-9451-2b1f78c5e9d0">



### Result 패턴 사용 시 효과
* enum과 동일하게 switch 문과 조합하여 case를 강제할 수 있다.
* 3개 이상의 성공과 실패를 처리할 수 있다.

<br></br>

## freezed 라이브러리
freezed = json_serializable + Equatable(==, hashCode, toString, copy) + immutable
* 선언된 필드들의 getter를 만들어서 외부에서 값을 변경할 수 없도록 한다.
* sealed class 작성을 편하게 해준다.

```dart
dart pub add freezed
```

* ver. 1
```dart
import 'package:freezed_annotation/freezed_annotation.dart';

part 'result.freezed.dart';

@freezed
sealed class Result<T> with _$Result<T> {
  const factory Result.success(T data) = Success;
  const factory Result.error(Exception e) = Error;
}
```

✅ @freezed 를 사용하자 코드가 대폭 줄었다.
✅ 코드 생성 후 빌드 명령어를 입력 해준다.

```dart
dart run build_runner build
```

* ver. 2
```dart
import 'package:freezed_annotation/freezed_annotation.dart';

part 'result_ver_2.freezed.dart';

@freezed
sealed class Result<D, E> with _$Result<D, E> {
  const factory Result.success(D data) = Success;
  const factory Result.error(E error) = Error;
}
```
D: 데이터  
E: 에러  
기본 버전에는 Exception만 처리하는 반면,  
신 버전에서는 원하는 에러 타입 정의 가능

```dart
enum NetworkError {
  requestTimeout,
  unknown,
}

// repository 에서 Result 타입을 반환하도록 수정
abstract interface class PhotoRepository {
  Future<Result<List<Photo>, NetworkError>> getPhotos();
}

class PhotoRepositoryImpl implements PhotoRepository {
  final MockPhotoApi _api;

  PhotoRepositoryImpl(this._api);

  @override
  Future<Result<List<Photo>, NetworkError>> getPhotos() async {
    try {
      final List<PhotoDto> photoDtoList =
          await _api.getPhotos('').timeout(Duration(seconds: 10));

      return Result.success(photoDtoList.map((e) => e.toPhoto)).toList();

      // 두 가지 이상의 에러를 리턴할 수 있다.
    } on TimeoutException {
      return Result.error(NetworkError.requestTimeout);
    } catch (e) {
      return Result.error(NetworkError.unknown);
    }
  }
}
```

* 실제 에러 처리 부분
```dart
void main() async {
  final photoRepository = PhotoRepositoryImpl(MockPhotoApi());

  final result = await photoRepository.getPhotos();

  switch (result) {
    case Success<List<Photo>, NetworkError>():
      print(result.data);
    case Error<List<Photo>, NetworkError>():
      {
        switch (result.error) {
          case NetworkError.requestTimeout:
            print('타임 아웃');
          case NetworkError.unknown:
            print('알 수 없는 에러');
        }
      }
  }
}

```

### freezed 를 활용한 Data Clase (모델) 작성
<img width="553" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/c2398164-5a1d-460a-9fdc-15fab5a21111">


### 정리
* enum은 클래스만큼 자유롭지 않다.
* equals, hashCode 재정의 불가능
* sealed 클래스는 서브 타입을 봉인한다.
* sealed class는 패터 매칭을 활용하여 모든 서브 타입에 대한 처리를 하기 용이하다.
* Result 패턴은 여러 종류의 성공과 실패를 처리하기 용이한 패턴이다.
* 앱의 규모에 맞는 Result 패턴을 사용하자
* 소규모 ver 1로도 충분
* 다국어 지원 : ver 2


<br></br>

## (필수) 과제 1. 이미지 검색 API 검토
DataSource -  https://pixabay.com/  
가입하여 Image Search API 사용법을 터득할 것. PostMan 등을 활용하여 결과 확인. TIL 에 과정 정리

### pixabay 사용 설명서

<img width="115" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/504da3ee-8e9c-4aed-b9a2-8cc18e1b3b7e">

If you make use of the API, show your users where the images and videos are from, whenever search results are displayed. That's the one thing we kindly request in return for free API usage.
> 이미지 출처를 표기해야 한다.

Hotlinking  
Returned image URLs may be used for temporarily displaying search results. However, permanent hotlinking of images (using Pixabay URLs in your app) is not allowed. If you intend to use the images, please download them to your server first. Videos may be embedded directly in your applications. Yet, we recommend storing them on your server.
> 반환된 이미지 URL은 일시적으로 검색결과를 표시하는 데 사용될 수 있다.  
> 그러나 이미지의 영구적인 핫링크(앱에서 Pixabay URL 사용)는 허용되지 않는다.  
> 영구적으로 이미지를 사용하려면 먼저 서버에 저장하는 것을 추천

### 이미지 검색
#### 1. 이미지 검색을 위한 baseUrl
```dart
https://pixabay.com/api/
```

#### 2. 본인의 API 키를 추가한다.
```dart
https://pixabay.com/api/?key=43171022-dca0290df38de24cd7ba6ed14
```

### 3. 원하는 이미지를 필터하기 위해 `q` 뒤에 조건들을 붙여준다.
100자 이하로 입력 가능하다.
```dart
예시) q=flowers+cat+home&image_type=photo&pretty=true

flowers+cat+home : 꽃, 고양이, 집

image_type : 사진

pretty : JSON 코드를 이쁘게 들여쓰기
```

<br></br>

### Postman에서 결과 확인하기

1. `New`, `HTTP`를 클릭한다.
<img width="480" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/aae31589-40f2-4150-90ff-6a1bf5c6a740">
<img width="530" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/14332754-04cd-4525-ae62-06dcbaebee1b">


2. 이미지를 `GET`하기 위한 주소를 입력하고 `Send` 클릭
<img width="586" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/c0b393a4-b62d-46a8-b2c5-b1642ef583b5">

3. 통신이 완료되면 200 응답과 코드들이 출력된다.
<img width="585" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/3040e6a5-0c07-49fe-8c11-1d6c157cd95b">

4. 그 중 첫 번째 이미지
<img width="583" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/1cca39e3-6b24-4983-ae2f-f8f02ba9c292">


## 기타
```dart
sealed class ResultVer2<D, E> with _$ResultVer2<D, E> {}

return ResultVer2.error(NetworkError.unknown);
E 타입이기 때문에 enum 값을 그대로 넣을 수 있었다.
```
```dart
try {
  throw Exception()
} catch (e) {
  return ResultVer2.error(NetworkError.unknown);
}
```

try애 throw Exception() 을 넣으면 catch로 바로 가기 때문에 에러를 확인할 수 있다.
