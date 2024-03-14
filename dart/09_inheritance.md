## 상속 Inheritance
> 자바에서 상속이란 기존의 클래스를 재활용하여 새로운 클래스를 작성하는 자바의 문법 요소이다. 상속하는 클래스를 슈퍼클래스(부모클래스) 상속받는 클래스를 서브클래스(자식클래스)라고 한다.

클래스 생성시 `class 서브클래스 extends 슈퍼클래스` 와 같이 생성하여 부모의 속성을 상속받을 수 있다.

```dart
class SuperHero extends Hero {
  //부모의 생성자로 한번 생성을 해야한다.
  SuperHero({required super.name, required super.hp});
}

```

### 재정의 Override
슈퍼클래스로 부터 물려받은 기존 기능을 재정의 하고싶을때 @override를 붙여 명시해준다.
```dart
@override
void attack(){
  super.attack(); //부모 메서드 그대로 실행한다는 코드.
  print('추가로, 레이저 빔을 날렸다!');
}
```

#### 올바른 상속
올바른 상속은 “is-a 원칙” 이라고 하는 규칙에 따른 상속을 말한다
- SuperHero is a Hero (o)
- Inn is a King (x)

#### 잘못된 상속
현실 세계의 등장인물 사이에 개념적으로 is-a 관계가 되지 못 함에도 불구하고 상속을 사용한 경우가 “잘못 된 상속" 이다.

#### 잘못된 상속을 하면 안 되는 이유
- 클래스를 확장할 때 현실세계와의 모순이 생긴다
- 객체 지향(OOP)의 4대 특징 중 1가지 “다형성" 을 이용할 수 없게 된다
