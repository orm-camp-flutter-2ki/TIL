240308 (Fri)
플러터 과정 5일차
=================

변수들에 final을 붙이는 이유
-
-> final은 이용하는 이유는 코드 상에서 가독성을 높여 변동성 있는 변수와 고정으로 지정되는 변수의 차이를 내기 위함이다.

생성자의 오버로드
--

```dart
class Hero {
  // 클래스가 가지는 속성을 field, 멤버변수 라고 부름
  String name;
  int hp;
  String? sword;

  // 생성자 : 인스턴스를 만드는 방법을 제공
  Hero({
    this.name = '홍길동',
    this.hp = 100,
    this.sword,
  });
  ```
위와 같이 생성자가 있다면 생성자를 오버로드한 클래스는 몇개가 있을까?

```dart
final hero1 = Hero(name: '홍길동', hp: 100, sword: sword);
final hero2 = Hero(name: '전우치', hp: 100);
final hero3 = Hero(name: '손오공');
final hero4 = Hero(hp: 50, sword:sword);
final hero5 = Hero(name: '송아지', sword:sword);
final hero6 = Hero(hp: 50);
final hero7 = Hero(sword: sword);
final hero8 = Hero()
```
