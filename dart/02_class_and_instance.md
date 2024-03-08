# Class And Instance

> 클래스와 인스턴스


## 클래스(Class)
> 오브젝트를 가상세계용으로 구체화한 것 (틀, 뼈대)
- 필드(Field) : 클래스의 속성
- 메소드(Method) : 클래스의 동작 (함수)

 ```dart
// 클래스
Class Person {
  String name; // 필드
  int age; // 필드

  Person(this.name, this.age); // 생성자

  void walk() {} // 메소드
}
```

## 인스턴스(Instance)
> 클래스를 활용하여 메모리 상에 데이터를 만들어낸 것

```dart
// 인스턴스화
Person person = Person('초짜', 24);
print(person.name); // '초짜' 출력
```
