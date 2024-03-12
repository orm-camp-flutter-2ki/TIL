240308 (Fri)

플러터 과정 5일차


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
위와 같이 생성자가 있다면 생성자를 오버로드한 클래스는 몇 개

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
정답은 8개의 오버로드가 가능하다.
이처럼 초기값을 설정을 해준다면 오버로딩을 다양하게 할 수있다.

```dart
class Person{

}
```
이런 식으로 생성자가 만들어져도 오류가 발생하지 않고 기본 생성자는 있다고 판단한다.


Hero( this.name, this.hp, {this.sword});
일때 사용법은
Hero('ddd', 11);
과
Hero('ddd',hp:11, sword: sword);
이런 방식으로 사용이 가능하고
required를 붙인다면
필수로 사용해야한다.


static mehod
static 키워드는 변수나 메소드에 사용되며 static 키워드를 사용하면 클래스가 메모리에 로딩될 때 자동으로 생성이 된다. 즉, static은 instance에 귀속되지 않고 class에 귀속된다. 그래서 객체를 생성하지 않아도 사용이 가능하며 속도가 빠르다.


