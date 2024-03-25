## 데이터소스 Datasource

> 데이터소스(datasource)는 서버로부터 데이터베이스에 대해 연결을 구축하기 위해 사용하는 이름. DataSource에서 추출한 가공되지 않은 데이터를 -> 사용 가능한 데이터로 가공해야한다.

### 데이터 소스의 종류
- Text,File,JSON,XML,CSV,RDBMS,NoSQL 등등
- 주로 사용되는 것은 JSON이나, 회사마다 다르다!

### 데이터 가공
Json을 예로,서버에서 문자열 형태의 Json을 보내주면 먼저 Dart의 Map 형태로 바꿔야 한다. <br/>
 -> 이것을 jsonDecode 라고 한다.
 
```dart
fiinal String jsonString = '''{
  'userId': 1,
  'id': 1,
  'title': 'delectus aut autem',
  'completed': false
}'''
```
👆이것을 

👇이렇게

```dart
{
  'userId': 1,
  'id': 1,
  'title': 'delectus aut autem',
  'completed': false
}

```
-> jsonEncode를 하면 역순으로!

### 라이브러리

실제로는 http주소로 된 api를 사용하기에 라이브러리를 따로 추가해야한다.<br/>
https://pub.dev/packages/http

### 모범 답안
- api를 다루는 모델클래스는 이름_api.dart 와 같은 파일명으로 작성한다.

```dart
class TodoApi {
  //다수의 객체를 List안에 리턴.
  Future<List<Todo>> getTodos() async {
    final response =
        await http.get(Uri.parse('https://jsonplaceholder.typicode.com/todos'));

    if (response.statusCode == 200) {
      List json = jsonDecode(response.body);
      List<Todo> data = json.map((json) => Todo.fromJson(json)).toList();
      return data;
    } else {
      throw Exception('Response 에러');
    }
  }

   //한가지의 객체를 리턴.
  Future<Todo> getTodo(int id) async {
    final response = await http
        .get(Uri.parse('https://jsonplaceholder.typicode.com/todos/$id'));
    if (response.statusCode == 200) {
      Map<String, dynamic> json = jsonDecode(response.body);
      Todo data = Todo.fromJson(json);
      return data;
    } else {
      throw Exception('Response 에러');
    }
  }
}
```

`+` 형변환 번외 <br/>
  `List json = jsonDecode(response.body);` 👈이것과 <br/>
  `final json = jsonDecode(response.body) as List;` 👈이것은 같다는 사실!
