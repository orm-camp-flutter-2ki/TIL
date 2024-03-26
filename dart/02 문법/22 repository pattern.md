# Repository Pattern
![repository](https://github.com/yujiyeong/TIL/assets/149862753/766bb264-8d9d-46ef-b737-048b16af80d8)

- 데이터에 액세스하는 방법을 추상화한 디자인 패턴
- 응용 프로그램의 유연성과 테스트 용이성을 높이고, 데이터 소스의 변경에 유연하게 대응할 수 있는 디자인 패턴
- 데이터를 가져오고 저장하는 데 사용되는 중간 계층
- 데이터에 대한 접근을 캡슐화하여 외부에 노출되는 데이터의 양을 제한
- 데이터 소스에 대해 알 필요가 없으며, 데이터 소스가 변경되더라도 응용 프로그램의 다른 부분에 영향을 덜 미침(결합/연결성 낮게)
<br/>

## Repository 선언
```dart
abstract interface class UserRepository {
  // 웹 서버에서 데이터를 가져오는 메서드
  Future<List<User>> getUsers();
}
```
- `abstract interface` 를 사용하여 추상 클래스로 작성
<br/>

## data source Api
```dart
class UserApi {
  Future<List<User>> getUsersApi() async {
    http.Response response;
    try {
      response = await http
          .get(Uri.parse('https://jsonplaceholder.typicode.com/users'));
    } catch (error) {
      print('[Error]\n$error');
      return []; // 예외가 발생하면 빈 리스트를 반환하거나 다른 처리할 수 있다.
    }

    final List json = await jsonDecode(response.body);
    return json.map((e) => User.fromJson(e)).toList();
  }
}
```
- 가장 많이 사용하는 json 데이터형식을 가져오는 `fromJson()`, `jsonDecode()` 을 사용...
- http 사용  
- 시간이 걸리는 작업임으로 `Future / async / await` 을 사용...  
<br/>

## Repository implements
```dart
class UserRepositoryImpl implements UserRepository {
  final UserApi _userApi = UserApi();

  @override
  Future<List<User>> getUsers() async {
    return await _userApi.getUsersApi();
  }
}
```
- data source를 사용해 repository를 구현한 것  
<br/>

## main에서 호출
```dart
void main() async {
  // 다형성을 사용한 인스턴스 생성
  final UserRepository userRepository = UserRepositoryImpl();

  List<User> user = await userRepository.getUsers();
  
  user.forEach((print));
}
```
<br/>

## 장점
- 언제든지 데이터 소스를 변경할 수 있음
- 로직에는 큰 영향을 끼치지 않음 (연결성을 약하게 해 유연성을 높이는 것...)
- 책임과 역할이 분배(?)가 된다
<br/>
