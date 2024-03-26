## DataSource
### 데이터의 근간이 되는 원천 재료
  * 예시
  * 만두피에서 데이터 소스는 밀가루
  <img width="150" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/7a2f0dfa-bca7-4d1b-bfe3-aa3413b1c8f7">
  
  * 찰흙으로 집 만들기에서 데이터 소스는 흙
  <img width="100" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/5edf0e5f-07a3-4995-a7f0-ec64ec040e8f">
  
  * 주민등록증의 데이터 소스는 해당 사람의 정보

### 데이터 소스로 뭘 하지?
  * 만두를 만들거나 -> 만두 앱
  * 집을 만들거나 -> 부동산 앱
  * 주민등록증을 만들거나

✅ **DataSource에서 추출한 가공되지 않은 데이터를 사용 가능한 데이터로 변환**  
✅ **json이 Map이 되어 Class로 들어가는 것과 비슷하다.**

### DataSource의 종류
* Text
* File
* JSON
* XML
* CSV
* RDBMS
* NoSQL
* 기타 등등

<br></br>

## json과 데이터 클래스의 상호변환
* 데이터 조작을 쉽고 편하게
* 서버와 통신을 대부분 JSON으로 함

<img width="650" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/8a60c933-57fa-49a7-8ff6-12426b1a8a17">

**[1] JSON String**  
json 파일을 파일 입출력을 통해서 가져오면 json 데이터는 텍스트 데이터이기 때문에 String 형태로 들어온다.

**[2] json 자료형(자료형: Map<String, dynamic>)**  
json을 다루기 위해 Map<String, dynamic> 자료형을 사용한다.  
json 데이터는 키(key)와 값(value)으로 이루어져 있고 키(key)는 반드시 String이며 값(value)은 자료형이 정해져있지 않다.  
때문에 Map<String, dynamic> 자료형으로 모든 json 데이터를 다룰 수 있다.

**[3] json 객체(자료형: Object)**  
json 데이터를 파싱하여 얻은 객체, json 데이터가 들어갈 객체.  
json을 사용한다는 것은 결국 데이터를 최종 결과물인 객체로 생성해내는 것

<br></br>

### json String -> Map<String, dynamic> 자료형으로 변환

```dart
String jsonString = '''
  {
    "name" : "killdong",
    "age" : 26,
    "hobby" : "soccer",
  }
''';
```

```dart
Map<String, dynamic> jsonData = jsonDecode(jsonString);

print(jsonData['name']); // killdong
print(jsonData['age']);  // 26
```

<br></br>

### Map<String, dynamic> 자료형 -> 객체로 변환

```dart
class User {
  String name;
  int age;
  String hobby;
  
  User(this.name, this.age, this.hobby);

  User.fromJson(Map<String, dynamic> json)
  : name = json['name'],
  age = json['age'],
  hobby = json['hobby'];
}
```

```dart
void main() {
  Map<String, dynamic> jsonData = jsonDecode(jsonString);
  User user = User.fromJson(jsonData); // user 객체를 찍어낸다.
}
```

<br></br>

### 객체 -> json String으로 변환

```dart
class User {
  String name;
  int age;
  String hobby;

Map<String, dynamic> toJson() => {
  'name' : name,
  'age' : age,
  'hobby' : hobby
};
```

```dart
String jsonString = jsonEncode(user);
```

### json List String -> List<모델 클래스>

```dart
// json 코드를 List<dynamic> 으로 변환
final jsonList = jsonDecode(response.body) as List;

// jsonList 에 담긴 값들을 List<Todo> 에 담는다.
List<Todo> todoList = jsonList.map((e) => Todo.fromJson(e)).toList();
```

## http
* import 형태
```dart
import 'package:http/http.dart' as http;
```
* as + 별명
* 탑 레벨에 접근할 수 있다.(get())
* as http라고 적지 않으면 get() 함수만 적게 되는데, 너무 추상적이고 다른 개발자가 이 함수의 역할을 모를 수 있기 때문에 `as http`로 적어준다.

* 예시
<img width="752" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/551aa1cf-ded8-412d-9db3-1660b1eb35c1">

## 기타
* Object 클래스
  * 모든 객체의 근간이 되는 최상위 클래스
  * Object 타입에는 모든 객체 인스턴스를 담을 수 있다.

* dynamic
  * 런타임에 타입이 결정된다.

* Dart에서 인스턴스를 복사하기 위해선 직접 copyWith() 같은 메서드를 만들어야 한다.
* List에서 sort()를 하면 원본이 바뀐다.
```dart
final names = ['홍길동', '뽀로로', '철수', '영미'];
names.sort();
print(names); // [뽀로로, 영미, 철수, 홍길동]
```
* ==와 hashCode는 항상 함께 재정의하는 것이다.
