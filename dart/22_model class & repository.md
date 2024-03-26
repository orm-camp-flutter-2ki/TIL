## Model Class & Repository패턴

### Model

> Model이란? 별도의 기능을 가지지 않는 순수한 클래스 <br/> 데이터 소스를 앱에 필요한 형태로 변환하여 앱 개발을 편리하게 해주는 역할<br/>도메인 모델, Entity, DTO, POJO, 데이터클래스 등으로 불린다.

#### 모델링 방법
1. DDD (Domain Driven Design)
  - 유사한 업무의 집합
  - 특정 상황이나 특정 객체가 중심이 될 수 있음
  - 모델 클래스 = 도메인을 클래스로 작성한 것
2. ORM (Object-relational mapping)
  - 데이터소스가 DB인 경우 DB와 모델간 상호 변환을 도와주는 기법

#### 모델 클래스 작성 예시    
일반클래스
```dart
class User {
  final String name;
  final int age;

  User(this.name, this.age);

  @override
  String toString()=> 'User(name: $name, age: $age);
}
```
불변객체
```dart
//생성자에 const 사용
//인스턴스 생성시 const 키워드를 붙일 수 있게된다.
class User {
  final String name;
  final int age;

  const User(this.name, this.age);

  @override
  String toString()=> 'User(name: $name, age: $age);
}
```
immutable 명시(Flutter에서만 사용!)
```dart
@immutable
class User {
  final String name;
  final int age;

  const User(this.name, this.age);

  @override
  String toString()=> 'User(name: $name, age: $age);
}
```
factory 생성자
```dart
class User {
  final String name;
  final int age;

  factory USer.fromJson(Map<String, dynamic> json {
    return User(json['name], json['age']);
  }
  
  @override
  String toString()=> 'User(name: $name, age: $age);
}
```

### Repository 패턴
>데이터 저장소에 접근하는 객체를 추상화하고, 데이터 소스와의 통신을 담당하는 객체를 캡슐화 하는 디자인 패턴 <br/>

>비지니스 로직은 프로그램의 핵심이며, 데이터 레이어는 데이터를 저장하고 관리하는 역할을 하는데, 비지니스 로직과 데이터를 분리하는 것은 여러가지 이점이 있음


#### 책임과 역할
- 데이터 소스와 상호작용하여 데이터를 CRUD 하는 역할을 담당
- **데이터 캡슐화**
- **데이터 추상화**
- 데이터 접근제어
- 예외처리
