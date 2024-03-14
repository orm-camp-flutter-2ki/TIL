---
title: 011 Dart - 다형성
author: Kim Donghyeok
created_at: 2024-03-14
updated_at: 2024-03-14
tags:
  - 생존코딩
  - 오름캠프
  - dart
---

# 다형성

다형성 (polymorphism) 이란 하나의 객체가 여러 타입을 가질 수 있는 것을 의미함

## 다형성을 활용하는 방법

선언을 상위 개념으로 인스턴스 생성은 하위 개념으로 한다.

**추상적인 선언 = new 상세정의**

```dart
Charcter chracter = Hero('홍길동', 100);
```

공통 행동에 대해서 인터페이스를 만들고 해당 인터페이스를 상속하게 하면 해당 인터페이스를  참조변수로 선언하여 사용 가능힘.

참조변수의 자료형은 컴파일러에게 이런 유형(타입)을 가질 수 있다고 알려주는 것

컴파일러는 실제로 객체가 어떤 것인지는 보지 못함.

### 상속 관계에서 다형성 구현

```dart
abstract class Character {
 //...
 String name;
 int level;
}
```

```dart
class Hero extends Character {
//...
}
```

```dart
void main() {
 Character hero = Hero('홍길동', 100);
}
```

### 구현 관계에서 다형성 구현

```dart
abstract intreface class Human {
 void speak();
} 
```

```dart
class Dancer implements Human {
 //...

 @override
 void speak() {
  print('댄서가 말을 합니다.');
 }
}
```

```dart
void main() {
 Human dancer = Dancer();
}
```

## 다형성 실패

다형성은 어떤 클래스가 상속(extends) 또는 구현 (implements) 했을 때 사용.

해당하는 관계에 있는 부모 클래스 / 인터페이스를 사용하여 다형성을 구현 할 수 있다.

```dart
Charcter chracter = Hero('홍길동', 100); // OK

Sword sword = Hero('name', 100); // NG
```

부모 클래스의 타입으로 자식 클래스의 인스턴스를 생성한 후 메소드를 호출 할 때 메소드 호출이 불가능한 경우가 발생했다

왜 그런걸까?

```dart
Wand wand = Wand('지팡이', 80);  
Wizard wizard = Wizard(name: '마법사', hp: 100, mp: 50, wand: wand);  
Slime slime = Slime(suffix: 'A');  
  
Character character = wizard; // 실제로 IDE에서 에러 발생, 할당 가능한다고 가정했을 떄

wizard.attack(slime);  
wizard.fireball(slime); // 이 메소드 호출 불가능
```

> `wizard.fireball()` 왜 안되는 걸까 ?
>
> `line:11` 에서 컴파일러가 Character 객체를 생성할 때 (사실상 레퍼런스 변수)  
> 이미 생성되어 있는 `wizard` 객체의 메소드까지 확인하지 않고  (생성된 객체의 내부를 확인 하지 않음)
> `character` 에 assign 되는 wizard 객체가 Character 클래스를 상속한 클래스 인지만  검사하여 assign 해주기 때문에 assign 이 되지만 (실제로는 IDE에서 차단)
>
> `line:24` 에서 실제로 메소드를 사용하려고 하면 Character 클래스에는 `fireball()` 메소드가 없어서 호출이 불가능 한 것이다  

## 타입 캐스팅

위와 같은 문제가 발생 했을 때 타입 캐스팅를 통해서 문제를 해결할 수 있다.

```dart
void main() {
 Monster monster = Slime(suffix: 'B');
 Slime slime = monser as Slime;
}
```

타입 캐스팅은 실제로 상속 관계에 있는 클래스사이에서 가능하며 형제관계에 있는 클래스들 간에는 타입캐스팅이 불가능하다.

```dart
void main() {
 Character character = Wizard(name: '마법사', hp: 100, mp: 50, wand: wand);  
 Hero hero = character as Hero; // 형제관계 타입캐스팅 불가능
}
```

## 인스턴스 타입체크와 smart cast

`is` 키워드를 통해 인스턴스의 타입을 체크 할 수 있다.

```dart
void main() {
 Character character = Wizard(name: '마법사', hp: 100, mp: 50, wand: wand); // smart cast
 if(character is Hero) {
  Hero hero = character;
 }
}
```

---

# 정리

부모 타입으로 인스턴스 생성

- 상속에 의한 is-a 관계가 성립 한다면, 인스턴스를 부모 클래스 타이브이 변수에 대입 할 수 있다.
- 부모 클래스 타입 변수에 대입하는 것으로, 퉁 칠 수 있음(?)

상자의 타입 과 내용의 타입의 역할

- 어떤 멤버를 이용할 수 있는가는 상자의 타입이 결정한다.
- 멤버가 어떻게 움직이는지는 내용의 타입이 결정한다.

취급 변경

- `as` 키워드를 사용하여 타입 캐스팅을 수행한다.
- `is` 키워드를 사용하여 타입을 검사할 수 있다.

다형성

- 같은 부모를 가지는 다른 인스턴스를 동일시 하여, 부모클래스 타입의 자료구조에 담을 수 있다.
- 마찬가지로, 부모 클래스 타입의 인수나 리턴 값을 이용하여, 다른 클래스를 모아서 처리 가능
- 동일시 취급해도, 각가의 인스턴스는 각 클래스를 따르고 다른 동작을 한다.
