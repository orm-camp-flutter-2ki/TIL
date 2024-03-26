## Model Class의 책임과 역할

* View에 보여질 데이터를 담는 객체
* 비슷한 용어들
  * 도메인 모델
  * Entiity
  * DTO
  * POJO
  * 데이터 클래스(toString, 생성자 등의 6종 세트 포함)

* 모델링 방법
* DDD(Domain Driven Design)
* ORM(Object-relational mapping)

* 모델 클래스 작성 예시
* 일반 클래스
```dart
class User {
  final String name;
  final int age;
  
  User(this.name, this.age);
}
```

* 불변 클래스
```dart
class User {
  final String name;
  final int age;
  
  const User(this.name, this.age);
}
```

* factory 생성자
```dart
class User {
  final String name;
  final int age;
  
  factory User.fromJson(Map<String, dynamic> json) {
    return User(json['name'], json['age']);
  }
}
```

## Model Class의 디자인 패턴
### Factory 패턴
### Singleton 패턴


## Repository 패턴
