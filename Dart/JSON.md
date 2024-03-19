## 📖 JSON
<br>

- 네트워크 통신에서 가장 많이 사용
- \[]로 리스트, {}로 객체를 표현
- Key : Value의 형태
- Dart의 Map<String, dynamic>과 똑같이  생김
<br>

### 📄 직렬화 역직렬화

```dart
class Departemnet {

  String name;

  Employee leader;

  Departemnet(

    this.name,

    this.leader,

  );

  Departemnet.fromJson(Map<String, dynamic> json) 
  // 역직렬화 Map으로부터 객체를 생성하는 생성자
      : name = json['name'],

        leader = json['leader'];

  

  Map<String, dynamic> toJson() => { 
  // 직렬화 객체를 Json 형태로 표현하는 메서드
        'name': name,

        'leader': leader.toJson(),

      };

}
```

```dart
void main() {

  String jsonString = '{"name":"총무부","leader":{"name":"홍길동","age":41}}';

  Map<String, dynamic> json = {

    "name": "총무부",

    "leader": {"name": "홍길동", "age": 41}

  };

  Map<String, dynamic> json2 = jsonDecode(jsonString); // Json을 Map으로 변환

  String jsonString2 = jsonEncode(json); // Map을 Json으로 변환

  

  print(json);

  print(json2); // json과 json2의 실행 결과가 같음

  print(jsonString);

  print(jsonString2); // jsonString과 jsonString2와 실행 결과가 같음

}
```

