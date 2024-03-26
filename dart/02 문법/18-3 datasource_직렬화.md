# Data Source를 데이터로 만들기
## http install
[[🔗pub.dev - http]](https://pub.dev/packages/http)
```dart
$ dart pub add http
$ flutter pub add http
```
![image](https://github.com/yujiyeong/TIL/assets/149862753/27e84468-583a-4d92-91e6-36918a99dec9)

- IDE terminal에 복사 붙여넣기를 해준 다음, `pubspec.yaml`에 잘 들어갔는지 확인한다. 없다면 `pub get` 버튼을 클릭한다.  


## import  
```dart
import 'package:http/http.dart' as http;
```
- `as http` : http 패키지의 이름을 http로 지정하고, 이를 사용하여 http 패키지의 클래스 및 함수를 호출한다. 코드의 가독성을 높이고, 패키지의 이름이나 충돌을 피할 수 있다.
<br/>

## data class 작성
- final keyWord
- fromJson(), toJson()
- toString override
- == operator & hashCode override
- withCopy (deep Copy)
<br/>

### final keyword
[[🔗 json 연습 데이터 페이지]](https://jsonplaceholder.typicode.com/)
```dart
class Todo {
  final int userId;
  final int id;
  final String title;
  final bool completed;

Todo({
    required this.userId,
    required this.id,
    required this.title,
    required this.completed,
  });
```
<br/>

### fromJson()
```dart
  Todo.fromJson(Map<String, dynamic> json) // 생성자
      : userId = json['userId'],
        id = json['id'],
        title = json['title'],
        completed = json['completed'];
```
- jsonDecode()
- String 형태의 json 데이터를 map으로 변환한다.
<br/>

### toJson()
```dart
  Map<String, dynamic> toJson() => // 함수
      {
        'userId': userId,
        'id': id,
        'title': title,
        'completed': completed,
      };
```
- jsonEncode()
- map 형태의 데이터를 String 형태의 json으로 변환한다.
<br/>

### toString override
```dart
  @override
  String toString() {
    return 'User{userId: $userId, id: $id, title: $title, completed: $completed}';
  }
```
- `cmd` + `n` : 자동 생성
<br/>

### == operator, hashCode override
```dart
  @override
  bool operator ==(Object other) =>
      identical(this, other) ||
      other is Todo &&
          runtimeType == other.runtimeType &&
          userId == other.userId &&
          id == other.id &&
          title == other.title &&
          completed == other.completed;

  @override
  int get hashCode =>
      userId.hashCode ^ id.hashCode ^ title.hashCode ^ completed.hashCode;
```
- `cmd` + `n` : 자동 생성
<br/>

### withCopy (deepCopy)
```dart
  Todo copyWith({
    required int? userId,
    required int? id,
    required String? title,
    required bool? completed,
  }) {
    return Todo(
      userId: userId ?? this.userId,
      id: id ?? this.id,
      title: title ?? this.title,
      completed: completed ?? this.completed,
    );
  }
```
<br/>

## http Api
```dart
import 'package:http/http.dart' as http;
import 'dart:convert';
```
```dart
class TodoApi {
  // http.get()을 사용하여 웹 서버에서 데이터를 가져오는 메서드
  Future<List<Todo>> getTodos() async {
    final response =
        await http.get(Uri.parse('https://jsonplaceholder.typicode.com/todos'));

    // 가져온 http 데이터를 map(), toList를 활용하여 데이터로 변환
    final List jsonList = jsonDecode(response.body);

    // Future<List<Todo>>를 반환, 비동기 작업이 완료되면 해당 데이터를 사용할 수 있다.
    return jsonList.map((e) => Todo.fromJson(e)).toList();
  }

  // http.get()을 사용하여 특정 ID에 해당하는 데이터를 가져오는 메서드
  Future<Todo> getTodo(int id) async {
    final http.Response response = await http
        .get(Uri.parse('https://jsonplaceholder.typicode.com/todos/$id'));

    // response.body == Json String
    final Map<String, dynamic> json = jsonDecode(response.body);

    // Future<Todo>를 반환, 비동기 작업이 완료되면 해당 데이터를 사용할 수 있다.  
    return Todo.fromJson(json);
  }
}
```
- 위 getTodos와 getTodo에서 Future을 사용하는 이유
- 시간이 걸리는 작업을 수행할 때 프로그램이 작업의 완료를 기다리지 않고 다른 작업을 수행하기 위해서..
- http.get을 통해 비동기적으로 웹 요청을 보내고, 해당 요청이 완료될 때까지 기다리는 데 Future를 사용함
  <br/>
  
```dart
  // TodoApi 클래스의 인스턴스
  final TodoApi todoApi = TodoApi();

  await todoApi.getTodo();
  await todoApi.getTodo(1); // 특정 ID에 해당하는 데이터 

  // await, 앞의 비동기 작업이 끝나기를 기다리는 중...
  // 정상적으로 받아지면 todos 변수에 List 형태로 담긴다.
  final List<Todo> todos = await todoApi.getTodos();
```
<br/>


