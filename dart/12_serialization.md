# Serialization, 직렬화

**직렬화**란 객체를 통신하기 쉬운 포맷으로 변환하는 것을 의미합니다.
**직렬화**의 경우는 보통 클래스를 Json, XML 등의 파일로 변환합니다.
이에 반대되는 개념이 **역직렬화**로, Json 파일을 클래스에 맞게 변환합니다.
Dart에서는 이를 어떻게 구현하는지 알아보겠습니다.

### 직렬화 (Serialize)
```dart
class Hero {
  String name;
  int age;
  int power;
  Hero(this.name, this.age, this.power);
  
  Map<String, dynamic> toJson() => { // 직렬화
    'name': name,
    'leader': age,
    'power': power
  };
}
void main() {
  Hero hero = Hero('히어로', 30, 100);
  print(hero.toJson());
  // {name: 히어로, age: 30, power: 100} 출력
}
```
toJson()을 사용해서 클래스를 Json 형태로 직렬화했습니다.
실제로 Dart상에서는 Map 타입입니다.

### 역직렬화 (Deserialize)
```dart
class Hero {
  String name;
  int age;
  int power;
  Hero(this.name, this.age, this.power);
  
  Hero.fromJson(Map<String, dynamic> json) // 역직렬화
    : name = json['name'],
      age = json['age'],
      power = json['power'];
  
  Map<String, dynamic> toJson() => { // 직렬화
    'name': name,
    'age': age,
    'power': power
  };
}
```
Class.fromJson과 같은 Named Constructor를 통해 Map으로 들어오는 Json을 클래스에 맞게 적용할 수 있습니다.
