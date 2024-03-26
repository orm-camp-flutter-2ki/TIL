# Model

#### Model 클래스란?
- 모델 객체 클래스의 속성에 대한 데이터를 조회할 수 있는 클래스
- 별도의 기능을 가지지 않는 순수한 클래스
- 데이터 소스를 앱에 필요한 형태로 변환하여 앱 개발을 편리하게 함

**기본적인 형태**
```dart
class User {
  final String name;
  final String email;
  
  User(this.name, this.email);
}
```

**불변**
```dart
class User {
  final String name;
  final String email;
  
  const User(this.name, this.email); // const 키워드 사용
}
```

**@immutation 어노테이션 사용(불변)**
```dart
@immutable // 불변이 아닌 경우 경고 표시
class User {
  final String name;
  final String email;
  
  const User(this.name, this.email);
}
```

**factory 생성자**
```dart
class User {
  final String name;
  final String email;
  
  User(this.name, this.email);
  
  factory User.fromJson(Map<String, dynamic> json) {
    return User[json['name'], json['email']);
  }
  
}
```

프로젝트의 성격에 따라 다양한 방식으로 모델 클래스를 정의할 수 있으며
필요에 따라 operator ==, toString() 등을 재정의 할 수도 있고
copyWith같은 Deep copy 메소드를 작성할 수도 있습니다.
