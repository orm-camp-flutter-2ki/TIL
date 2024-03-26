## 1. factory 생성자

-생성자를 만드는 새로운 방법

-팩토리는 리턴이 있어야 됨.

-해당 클래스의 새 인스턴스를 항상 생성하지 않는 생성자를 구현할 때 사용

- factory 패턴
- singleton 패턴

## 2. repository 패턴

소프트웨어 개발에서 데이터 저장소에 접근하는 객체를 추상화하고,

데이터소스(DB, File 등)와의 통신을 담당하는 객체를 캡슐화 하는 디자인 패턴임.

데이터 소스와 상호작용하여 데이터를 추가, 조회, 수정, 삭제하는 역할을 담당

- **확장을 고려한 repository 패턴 작성(인터페이스 정의를 통한 추상화)**

```dart
abstract interface class UserRepository {
Future<User> findUserById(String id);
Future<List<User> findAllUser();
Future<User> saveUser(User user);
Future<void> deleteUser(String id);
}
```

- **인터페이스 구현체 작성은 똑같이 impliments 하고, 오버라이드해서 작성**

```dart
class UserRepositoryImpl implements UserRepository {
final _database = SqliteDatebase('users.db');

@override
Future<User> findUserById(String id) async {
if(result.isEmpty) {
return null;
}
return User(results[0]['id'], result[0]['name'], result[0]['age'];
```
