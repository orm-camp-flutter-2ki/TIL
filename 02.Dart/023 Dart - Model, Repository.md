---
title: 023 Dart - Model, Repository
author: Kim Donghyeok
created_at: 2024-03-26
updated_at: 2024-03-26
tags:
  - 생존코딩
  - 오름캠프
  - dart
---

# Model Class, Repository

## Model 클래스

```dart
class User {
 final String name;
 final String email;

 User(this.name, this.email);
}
```

Model class 의 책임과 역할

- 순수한 클래스
- 데이터 소스를 저장하는 개념
- View에 보여질 데이터를 담는 객체

비슷한 용어들

- 도메인 모델
- Entity
- DTO
- **데이터 클래스**

## 모델링 방법

- DDD (Domain Driven Design)
- ORM (Object-realtional mapping)

### DDD (Domain Driven Design)

유사한 업무의 집합

특정 상황, 특정 객체가 중심이 될 수 있음

Model Class = 도메인을 클래스로 작성하는 것

### ORM (Object-realtional mapping)

데이터 소스가 DB 인 경우 DB 와 모델간 상호 변환을 도와주는 도구

ORM은 DB를 활용할 경우에 따로 살펴봐도 됨

## 모델클래스

### 일반 클래스

```dart
class User {
 final String name;
 final int age;
 
 User(this.name, this.age);
 
 @override
 String toString() => User(name:$name, age: $age);
}
```

### 불변클래스

```dart
class User {
 final String name;
 final int age;
 
 const User(this.name, this.age);
 
 @override
 String toString() => User(name:$name, age: $age);
}
```

- 모든 필드의 값이 final (불변) 일때 생성자를 const 로 선언하여 불변 클래스로 만들어 준다.
- 불변클래스로 인스턴스를 생성 했을 때 hashCode 값이 동일하다
- identical() 로 메모리 주소를 검사해도 동일

> 대표적인 불변객체는 String 이다, String literal 로 동일한 문자열을 선언 했을 때 두 문자열은 identical 하다.
>
> int 형 타입의 변수를 동일한 value 로 두 개 선언했을 때 두 변수도 identical 하다.
>
> 메모리에 저장된 값(value)들은 기본적으로 재사용되는 것을 가정함. (메모리 재활용)
>
> const 생성자가 호출될 때 런타임에서 모든 값들이 불변임이 보장되어야 생성자에 변수가 전달된다.
>

### @immutable

```dart
class User {
 final String name;
 final int age;
 
 const User(this.name, this.age);
 
 @override
 String toString() => User(name:$name, age: $age);
}
```

- 클래스에 @immutable 어노테이션을 붙이면 불변이 아닌 경우 경고가 표시됨

### factory 생성자

```dart
class User {
 final String name;
 final int age;
 
 factory User.fromJson(Map<String, dynamic> json) {
  return User(json['namel'], json['age']);
 }
 
 @override
 String toString() => User(name:$name, age: $age);
}
```

- 생성자 본문을 사용하여 인스턴스를 return 하는 생성자를 만들 수 있다.
- initializer list 를 사용할 수 없음
- Factory 패턴, Singleton 패턴 등으로 응용할 수 있다.

## Factory 패턴

인스턴스를 만드는 패턴

![[240326_factory_pattern.png]](/02.Dart/_resources/240326_factory_pattern.png)

마치 공장과 같이 요청에 따라 인스턴스를 생성하여 반환,

## Singletone 패턴

한 개의 인스턴스만 생성되는 것을 보증 하기위한 패턴

인스턴스 생성을 여러번 시도해도 한 개의 인스턴스가 공유됨

캐시, 공유데이터, 처리의 효율화 등에 사용되는 패턴

![[240326_singleton_pattern.png]](/02.Dart/_resources/240326_singleton_pattern.png)

```dart
class RentCar {  
  // static 인스턴스를 미리 생성  
  static final RentCar _instance = RentCar._internal();  
  int count = 0;  
  
  void increment() {  
    count++;  
  }  
  
  // 기본생성자는 클래스 내부에 생성자 정의가 없어야 함  
  // private 생성자이므로 외부에서 인스턴스 생성을 할 수 없게 함  
  RentCar._internal();  
  
  // 기본생성자를 factory 로 만들어 줌  
  factory RentCar.getInstance() {  
    return _instance;  
  }  
}  
  
void main() {  
  final instance1 = RentCar.getInstance();  
  final instance2 = RentCar.getInstance();  
  
  print(identical(instance1, instance2)); // true  
}
```

> **factory와 singleton 은 엄연히 다르다!**
>
> **factory가 singleton을 구현하는데 사용되지만, factory가 singleton 패턴이라고 말할 수 없다**

## Repository 패턴

소프트웨어 개발에서 데이터저장소에 접근하는 객체를 추상화하고,  
데이터소스(DB, File 등) 와의 통신을 담당하는 객체를 캡슐화 하는 디자인 패턴

![[240326_repository_pattern.png]](/02.Dart/_resources/240326_repository_pattern.png)

### Repository의 책임과 역할

- 데이터 소스와 상호작용 하여 **데이터를 추가, 조회 수정,삭제 (CRUD) 하는 역할을 담당**
- **데이터 캡슐화**
- **데이커 추상화**
- 데이터 접근 제어
- 예외 처리

### Repository 패턴의 이점

 데이터를 저장하고 관리하는 역할, 비즈니스 로직과 데이터를 분리하는 것은 여러 이점이 있음

- 데이터 조작을 캡슐화하여 다형성 이용 가능
- 유지 관리성 향상
- 재사용성 향상
- 테스트 용이성 향상
- 확장성 향상
- **데이터 엑세스 추상화**

### Repository 패턴의 추상화

Repository 를 인터페이스로 만들어서 추상화 한 다음  다형성을 이용해 이 인터페이스를 구현하는 다양한 레포지토리를 만들어서 특정한 기능을 위한 RepositoryImpl 을 만든다.

```dart
abstract interface class UserRepository {  
  Future<User> findUserById(String id);  
  Future<List<User>> findAllUsers();  
  Future<User> saveUser(User user);  
  Future<void> deleteUser(String id);  
}
```

```dart
class UserRepositoryImpl implements UserRepository {
  Future<User> findUserById(String id) {...}
  Future<List<User>> findAllUsers() {...}  
  Future<User> saveUser(User user) {...}  
  Future<void> deleteUser(String id) {...}  
}
```
