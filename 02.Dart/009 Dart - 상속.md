---
title: 009 Dart - 상속
author: Kim Donghyeok
created_at: 2024-03-12
updated_at: 2024-03-12
tags:
  - 생존코딩
  - 오름캠프
  - dart
---

# 상속 (Inheritance)

"이전에 만든 클래스와 닮았지만, 일부 다른 클래스" 를 만들 필요가 있을 경우가 늘어남  

기존 코드 복사 붙여넣기의 문제점

- 추가, 수정에 시간이 걸림
- 소스의 파악이나 관리가 어려워짐

> 해결책으로 "상속" 을 활용

```dart
class Person {  
 String name;  
 int age;  
   
 Person({required this.name, required this.age}) {  
  print('Person 클래스의 생성자를 호출');  
 }  
   
 run() {  
  print('사람이 달립니다.');  
 }  
}
```

```dart
class Male extends Person {  
 String gender = '남성';  
   
 Male({required super.name, required super.age}) {  
  print('Male 클래스의 생성자를 호출');  
 }  
   
 @override  
 run() {  
  print('이름이 ${super.name} 인 남성이 달립니다.');  
 }  
}
```

## 상속관계의 표현방법

![[240312_inheritance_expression.png]](/02.Dart/_resources/240312_inheritance_expression.png)

## 오버라이드 (override)

기존 기능을 재정의

> Dart 에서는 오버로딩 (overloading) 을 지원하지 않음

```dart
@override
run() {
 print('이름이 ${super.name} 인 남성이 달립니다.');
}
```

## super

super 키워드로 부모 객체를 참조한다.

```dart
// super 키워드로 부모 객체의 필드를 참조하여 생성자 선언
Male({required super.name, required super.age}) {  
 print('Male 클래스의 생성자를 호출');      
}  
```

## 상속과 생성자

자식 클래스의 인스턴스가 생성될 때 부모 클래스의 생성자가 호출된 후 자식 클래스의 생성자가 순차적으로 호출

자식클래스는 부모 클래스로부터 생성자를 상속 받지 않는다.

생성자를 선언하지 않은 자식 클래스는 이름과 인자가 없는 디폴트(default) 생성자 만을 가진다.

```dart
void main() {
 final Male man = Male(name: '슈퍼맨', age: 200);
}

// 출력
// Person 클래스의 생성자를 호출
// Male 클래스의 생성자를 호출
```

> **생성자를 호출하지 않았을 경우 에러가 나는 이유**  
>
> Dart에서 생성자를 선언 하지 않았다면, 디폴트(default) 생성자가 주어진다.  
> 디폴트 생성자는 인자가 없고, 부모 클래스의 디폴트 생성자를 호출한다.  
> 부모 클래스에 디폴트 생성자가 없다면 에러가 발생한다.

## 올바른 상속

올바른 상속은 ***"is-a 원칙"***  이라고 하는 규칙에 따른 상속을 말한다.

![[240312_inheritance_expression.png]](/02.Dart/_resources/240312_inheritance_expression.png)

> SuperHero is a Hero
>
> (SuperHero 는 Hero 의 한 종류이다.)

## 잘못 된 상속

현실 세계의 객체들 사이에 **개념적으로 is-a 관계가 되지 못함에도 불구하고 상속을 사용한 경우가 "잘못 된 상속"**

잘못된 상속을 하면 안되는 이유

- 클래스를 확장할 때 현실세계와의 모순이 생긴다.
- 객체 지향의 3대 특징 중 1가지 "다형성" 을 이용할 수 없게 된다.

## 구체화와 일반화의 관계

자식 클래스 일 수록 **구체화** 되고  
부모 클래스 일 수록  **추상적**인 것으로 **일반화** 된다.

![[240312_abstraction_genalization.png]](/02.Dart/_resources/240312_abstraction_genalization.png)

---

# 정리

상속의 기초

- `extends` 를 사용하여 기존 클래스를 기초로 하는 새로운 클래스를 정의할 수 있다.
- 부모 클래스의 멤버는 자동적으로 자식 클래스에 상속 되므로 자식 클래스에는 추가된 부분만 기술하면 된다.
- 부모 클래스에 있느 메소드를, 자식 클래스에서 재작성 할 경우 이것을 **오버라이드** 한다고 한다.
- 올바른 상속이란  "자식 클래스 is-a 부모 클래스"
- 상속에는 "추상적, 구체적" 관계가 있다는 것을 정의하는 역할 도 있음

인스턴스

- 인스턴스 내부에는  부모클래스의 인스턴스를 가지는 다중구조를 가진다.
- 보다 외측의 인스턴스에 속하는 메소드가 우선적으로 동작한다
- 외측의 인스턴스에 속하는 메소드는 super 를 사용하여 내측 인스턴스의 멤버에 접근 할 수 있다.

생성자 동작

- 다중구조의 인스턴스가 생성되는데, 자동적으로 가장 외측 인스턴스의 생성자가 호출됨
- 모든 생성자는, "무보인스턴스의 생성자" 를 호출할 필요가 있다.
