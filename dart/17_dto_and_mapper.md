# Dto, Mapper

### Dto (Data transfer object)
Dto는 데이터 소스를 모델 클래스로 변환하는 과정에서
순수하게 클래스에 담기 위한 중간 전달 객체입니다.

Dto가 도입된 이유로는 받아오는 Json에서 null이나 예외의 경우 때문에 에러가 나타나는 것을 방지하기 위해서입니다.
Dto를 사용하여 Map에서 Model로 변환할 때 null과 예외의 경우를 사전에 간편히 걸러낼 수 있습니다.

**모델 클래스와의 차이점**
```dart
Model
class User {
  final String name;
  final int age;
  
  const User({
    required this.name,
    required this.age
  });
  
  @override
  bool operator==() => ...
  @override
  int get hashCode => ...
  @oveerride
  String toString() => ...
  User copyWith({...});
}
```
```dart
Dto
class UserDto (
  String? name;
  int? age;
  
  UserDto({
    this.name,
    this.age
  });
  
  UserDto.fromJson(dynamic json) {
    name = json['name'];
    age = json['age'];
  }
)
```

Dto는 모든 필드가 Nullable 변수이며, 직렬화와 역직렬화를 제공합니다.
기존에는 Model에서 직렬화와 역직렬화를 구현하였지만
이를 Dto로 분리하여 역할도 나뉘고 안정적인 흐름을 줍니다.

따라서 Api 요청을 할 때의 흐름은 Api -> Dto -> Model 순서인데
Dto에서 Model로 변환하기 위해 주로 Mapper를 사용합니다.

### Mapper
toJson()도 Mapper라고 할 수 있겠습니다.
```dart
Mapper
extension UserDtoToUser on UserDto {
  User toUser() {
    return User(
      name: name ?? '익명',
      age: age ?? 0,
    );
  }
}
```
extension을 사용하여 안전하고, 로직을 처리할 수 있게 만들 수 있습니다.
Mapper는 Nullable 객체를 Non-Nullable 객체로 재구성해주는 역할을 합니다.
Dto 전체를 변환하지 않고 필요한 부분만 변환할 수 있습니다.
