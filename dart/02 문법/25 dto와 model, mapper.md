# DTO, model class, mapper
<div align="center">
<img src="https://github.com/yujiyeong/TIL/assets/149862753/bcbc6fe8-8659-4add-bc49-102a69f80289" width="700">
</div>

# DTO (Data Transfer Object)
> json -> Dto -> Model Class
- 데이터 소스를 모델 클래스로 **변환**하는 과정에서 순수하게 클래스에 담기 위한 **중간 전달 객체**

### 왜?
- 잘못된 데이터 소스 (Json)를 받더라도 안 터지게 하려는 클라이언트 개발자의 방어 수단
- Map -> Model Class 변환 시 null 값 등의 예외를 사전에 걸러내기 위한 것  

## 어떻게?
- 필드는 non-final, all nullable
- named 생성자
- fromJson() 
- toJson()

> `json to dart` plug-in 설치해서 dto 만들기

<div align="center">
<img width="550" alt="image" src="https://github.com/yujiyeong/TIL/assets/149862753/2acd4b24-1ea4-495e-b345-8c87bd208aa5">

<img width="550" alt="스크린샷 2024-03-28 오전 11 49 17" src="https://github.com/yujiyeong/TIL/assets/149862753/dfd6acd0-9526-4c2d-9c5b-0142d09b58f8">

<img width="600" alt="스크린샷 2024-03-28 오전 11 49 24" src="https://github.com/yujiyeong/TIL/assets/149862753/8ed155f0-2ecf-4724-8647-100894261d54">

</div>

<br/>

# model
- Fields: 데이터의 속성을 나타내는 멤버 변수  
- Constructor: 객체를 초기화하기 위한 메서드
- == operator: 두 객체가 동일한지 확인하는 == 연산자 재정의
- Hash code: 객체의 해시코드를 생성하는 메서드로, 동일한 객체에 대해 동일한 해시코드를 반환하는 메서드 재정의
- toString: 객체의 문자열 표현을 반환하는 메서드 재정의
- Copy With: 메서드는 불변성을 유지하면서 객체의 변경된 사본을 생성하는 메서드 (deep copy)

## 어떻게?
- 모든 필드가 final, non-nullable 상수
- == operator, hashCode
- toString()
- copyWith()
<br/>

# mapper
- 데이터 형식을 다른 데이터 형식으로 변환하는 과정
- 데이터베이스에서 데이터를 가져와서 애플리케이션에서 사용하는 형식으로 변환하거나,
외부 API와 통신할 때 데이터를 요청하고 응답을 처리하는 등의 작업에 사용

## 어떻게?
- 맵퍼는 Dto 를 모델 클래스로 변환하는 유틸 메소드로 확장함수 활용 추천
- 사용하기 편하도록 nullable 을 non-nullable로 변환하는 것이 핵심
- Dto 전체를 변환하는 것이 아닌, 필요한 부분만 변환
- 직접 수기로 작성하며 `extention - on`을 사용하여 기존 클래스에 새로운 기능을 추가하는 방식으로 생성
```dart
// GeoDto에 Geo를 반환하는 toGeo() 메서드를 만드는 것
// toGeo() : Geo 인스턴스를 만들어 반환한다.
extension GeoDtoToGeo on GeoDto {
  Geo toGeo() {
    return Geo(
      lat: lat ?? '0.0', // 변환되는 model 부분 : 뒤가 베이스 dto
      lng: lat ?? '0.0',
    );
  }
}

// Geo에 GeoDto를 반환하는 toGeoDto() 메서드를 만드는 것
// toGeoDto() : GeoDto 인스턴스를 만들어 반환한다.
extension GeoToGeoDto on Geo {
  GeoDto toGeoDto() {
    return GeoDto(
      lat: lat, // 변환되는 dto 부분 : 뒤가 베이스 model
      lng: lat,
    );
  }
}
```
## 형변환/변수명변경이 필요한 경우의 mapper
### case: num -> double
**Dto**
```dart
class StoreDto {
  num? lat;
  num? lng;
}
```
**model**
```dart
class Store {
  final Double lat; // 형 변환 필요
  final num longitude; // 변수명 변경 필요
}
```
**mapper**
```dart
extension StoreDtoToStore on StoreDto {
Store toStore() {
    return Store(
      lat: lat?.toDouble() ?? 0.0, // toDouble()을 사용해 형변환
      longitude: lng ?? 0.0, // 변수명 변겅
    );
  }
}

extension StoreToStoreDto on Store {
  StoreDto toStoreDto() {
    return StoreDto(
      lat: lat,
      lng: longitude, // 변수명 변경
    );
  }
}
```
### case: 클래스 내 필드에 접근
**Dto**
> Geo -> Address -> User
```dart
class UserDto {
  AddressDto? address;
}
```
```dart
class AddressDto {
  GeoDto? geo;
}
```
```dart
class GeoDto {
  String? lat;
  String? lng;
}
```
**model**
```dart
class User {
  final double latitude;
  final double longitude;
}
```
**mapper**
```dart
extension UserDtoToUser on UserDto {
  User toUser() {
    return User(
      latitude: double.tryParse(address?.geo?.lat ?? '0.0') ?? 0.0,
      longitude: double.tryParse(address?.geo?.lng ?? '0.0') ?? 0.0,
    );
  }
}
// tryParse() : String을 double로 변환할 수 있는지 시도하는 메서드
// latitude: double.tryParse(address?.geo?.lat ?? '0.0') ?? 0.0,
// latitude: double.tryParse(address!.geo!.lat!) ?? 0.0,
//  위의 두 코드는 같은(?) 코드, 변환 성공 시 해당 값을 반환하고 실패하면 null을 반환
// ! 또는 ?? 연산자를 사용하여 null이 아님을 확실히 보장(!)하거나, null일 때의 기본값을 설정


extension UserToUserDto on User {
  UserDto toUserDto() {
    return UserDto(
      name: name,
      email: email,
      address: AddressDto(
        geo: GeoDto(
          lat: latitude.toString(),
          lng: longitude.toString(),
        ),
      ),
    );
  }
}
```

