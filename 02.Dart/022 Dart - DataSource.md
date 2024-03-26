---
title: 022 Dart - DataSource
author: Kim Donghyeok
created_at: 2024-03-25
updated_at: 2024-03-25
tags:
  - 생존코딩
  - 오름캠프
  - dart
---

---

### 주요 내용

- import 에 `as` 를 이용해서 alias를 지정, top-level 함수도 alias를 통해 접근할 수 있음
  (어떤 패키지의 함수를 사용하는지 가독성을 높이기 위해서)
  
 ```dart
 import 'package:http/http.dart' as http;
 ```
  
- `http.get()` 는 top-level 함수 이지만 alias를 통해 접근할 수 있다.
- `Map<String, dynamic>` 형태로 변환되는 JSON 데이터, value에 해당하는 데이터의 type cast 가 필요하다.  

---

# 데이터 소스

데이터의 근간이 되는 원천 재료

프로그램이 사용하는 원천 데이터 모든 것이 해당 됨

DataSource 에서 추출한 가공되지 않은 데이터를 사용가능한 데이터로 변환

## DataSource 의 종류

- Text
- File
- JSON
- XML
- CSV
- RDBMS
- NoSQL

## JSON 데이터

오늘날, 대부분의 클라이언트-서버 간의 통신은 JSON 형태의 데이터로 이루어진다.

JSON 은 Key-Value 형태의 문자열 데이터로, Dart 의 `Map<K, V>` 과 형태가 유사하다

## JSON 과 데이터 클래스의 상호변환

```dart
class User {
 final String name;
 final String email;

 User(this.name, this.email);

 User.fromJson(Map<String, dynamic> json)
  : name = json['name'] as String,
    email = json['email'] as String;

 Map<String, dynamic> toJson() => {
  'name': name,
  'email': email,
 }
}
```

- `.fromJson()` 을 이용하여 `Map<String, dynamic>` 형태의 json 데이터를 객체로 역직렬화한다.
- `toJson()` 을 이용하여 객체를 직렬화 하여 `Map<String, dynamic>` 형태의 json으로 직렬화 한다.

![[240325_json_map_model.png]](/02.Dart/_resources/240325_json_map_model.png)

JSON을 Map 형태로 변환하여 키-값 형태로 데이터를 조작 할 수 있다.

JSON -> Map -> Model Class(데이터 클래스) 의 순서로 변환한다.

![[240325_json_map_model_add_method.png]](/02.Dart/_resources/240325_json_map_model_add_method.png)

### jsonDecode()

Json String을 Map으로 변환 해주는 함수

```dart
String jsonString = '''
{
  "id:": 1,
  "email": "kim@example.com",
}
''';

Map<String, dynamic> jsonDate = jsonDecode(jsonString);
```

> **JSON List String을 List<모델> 로 변경하려면 map() 함수를 활용함.**

```dart
const jsonStringList = '''
[
  {
    "id:": 1,
    "email": "kim@example.com",
  },
]
''';

final jsonList = jsonDecode(jsonListString) as List; // List<dynamic>
List<User> users = jsonList.map((e) => User.fromJson(e)).toList();
```

> `map()` 함수안에서 `User.fromJson()`을 해주는 이유
>
> `jsonList = jsonDecode(jsonListString) as List` 에서 `jsonList`의 타입은 `List<dynamic>` 이다,  
> 왜냐하면, `jsonStringList` 에서 `jsonDecode()`로 변환된 데이터를 런타임에서 `User` 로 추론할 수 없기 때문  
> 따라서, `jsonList` 내부의 원소 *(User 객체로 변환하고자 하는 데이터)* 를 `User.fromJson()` 을 통해  
> `dynamic` 을 `User` 타입으로 변환해주어야 한다.
