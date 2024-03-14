# 추상화와 인터페이스  
> 추상화 -> 인터페이스  
> 재사용성을 높여 휴먼에러를 줄일 수 있으며, 코드가 짧아져서 생산성, 가독성 높아짐   
<br/>

## 추상화(abstract)
- 추상클래스는 _이텔릭체(italic)_ 표기된다.  
- 추상클래스는 인스턴스화가 금지되어 있다.
- 다계층의 추상 상속 구조이며, 상위 객체일 수록 추상적이다. is a 관계가 성립된다.
<br/>

### 추상클래스 선언
`상속 extands`  
- 함수를 구현해도 되고, 구현하지 않아도 되며, 함수를 구현하고 안 하고의 구분은 중괄호`{}` 유/무로 구분한다.

```dart
abstract class Character { // class 앞에 키워드가 붙는다
  String name;
  int hp;
  
  Character(this.name, this.hp);

  // 메소드 구현
  void run() {
    print('$name은 도망쳤다.');
  };

  // 추상 메소드, 미구현
  void attack(Slime slime);
}
```
<br/>

### override 강제
- `extends`와 함께 사용하며, 자식(sub)클래스 생성 시 미구현되었던 메소드의 @override가 강제된다.  
- @override를 하고 싶지 않다면, 자식(sub)클래스도 추상화한다. 이 경우에도 인스턴스화는 금지된다.     

```dart
class Hero extends Character { // 추상 클래스 Character 상속
  Hero(super.name, super.hp);

  @override
  // 미구현 메소드, 이 부분의 override는 강제
  void attack(slime) {}

  @override
  // 구현된 메소드, 이 부분의 override는 강제가 아님
  void run() {
    super.run();
    print('$name의 명성이 떨어졌다.');
  }
}
```
<br/>

### 인스턴스(instance) 생성 불가
- 추상클래스는 인스턴스화 할 수 없다. 
![image](https://github.com/yujiyeong/TIL/assets/149862753/d2a26132-8847-4fa8-bbb9-36403b82aaaf)

```dart
void main() {
  Character character = Character(); // error, Character class는 abstract class이기 때문
}
```
<br/>

## 인터페이스 (interface)  
- 필드를 가지지 않으며, 모든 메소드는 추상 메소드여야 한다.  
- interface는 `abstract`와 함께 사용하며,(모든 메소드가 미구현 상태이기 때문에) `implements`와 함께 사용한다.  
- interface에서 특징(기능)을 정의하고, `implements`에서 구현한다.  
- 같은 인터페이스를 구현한 클래스들은 공통 메소드를 구현하고 있음을 보장한다.  
<br/>

### 인터페이스 선언
```dart
abstract interface class Thing {
// 메소드 정의 (구현 X)
}
```
<br/>

### 특별 기능  
- 여러 인터페이스를 다중으로 구현할 수 있다.  
```dart
class TangibleAsset extends Asset implements Thing, Name.... {
// 코드블럭
}
```
<br/>
