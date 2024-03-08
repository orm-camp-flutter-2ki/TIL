object와 instance
=============
> 객체 -> 클래스 -> 인스턴스

### 객체(object)  
- 소프트웨어 세계에 구현할 대상이다.  
- 클래스에 선언된 틀(설계도, 뼈대) 그대로 생성된 실체이다.   
- 하나의 클래스로부터 무수히 많은 객체를 생성할 수 있다.   
  
```dart  
class Person {
  String name;  // field 필드(멤버 변수, 전역 변수), camel case로 표기한다.
  int age;

  Person(this.name, this.age);  // this. : 나의.name, 나의.age
}
```
<br/>

### 인스턴스(instance)  
- 설계도를 바탕으로 소프트웨어 세계에 구현된 구체적인 실체이다.  
- 실체화된 인스턴스는 메모리에 할당된다.  
- 원본(추상적)으로부터 생성된 복제본을 의미한다.  

```dart
void main() {
    Person girt = Person('amy', 10);  // 생성자: 객체, 인스턴스를 만드는 것이다.
    Person boy = Person('jason', 14); // Person 클래스에 boy 객체, 인스턴스이다.
}
```
<br/>

