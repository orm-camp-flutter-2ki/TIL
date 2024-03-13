---
title: 010 Dart - 추상클래스와 인터페이스
author: Kim Donghyeok
created_at: 2024-03-13
updated_at: 2024-03-13
tags:
  - 생존코딩
  - 오름캠프
  - dart
---

# 정리

추상클래스

- 자식클래스의 공통적인 속성을 일반화, 추상화 하기 위해 만들어진 클래스
- 추상클래스의 사용을 통해 자식클래스는 부모클래스를 구체화 하고 기능을 확장
- 상속(`extends`) 키워드를 통해 사용
- 추상 클래스는 필드와 메소드 모두 가지고 있음
- 추상클래스가 가진 메소드 중 정의만 존재하고 구현이 되지 않은 메소드를 추상 메소드라고 부른다.
- 자식클래스에서 추상클래스를 상속할 때, 추상 메소드를 반드시 구현해야 한다.
- 다중상속 X

인터페이스

- 일반화, 추상화 가능한 클래스 집합에서 공통적으로 수행 가능한 동작들을  한데 묶은 것
- 인터페이스를 통해 구현체(구현 클래스) 에서 구현할 동작들을 강제함
- 구현(`implements`) 키워드를 통해 사용
- 인터페이스는 추상메소드만 가지고 있음, 필드 X
- 추상클래스와 마찬가지로 구현클래스는 추상메소드를 반드시 구현해야 함
- 다중 구현 O  

---

# 추상 클래스

추상화된 개념을 클래스로 만든 것  

상속은 기능의 확장을 목적으로 사용함, 부모 클래스의 개념이 모호할때 추상클래스를 활용한다.

추상클래스는 상속의 재료로 사용됨  

추상클래스는 상세부분이 미정의  

## 추상클래스와 추상 메소드

```dart
// 추상 클래스
abstract class Character {
 String name;
 in hp;

 Character(this.name, this.hp);

 void run() {
  print('$name이 도망쳤다.');
 }

 // 추상 메소드
 void attack(Slime slime);
}
```

## 추상클래스의 제약

#### 1. 오버라이드 강제

- 추상클래스에서 정의한 추상 메소드는 추상클래스를 상속한 자식 클래스에서 반드시 구현해야함

#### 2. 인스턴스화 금지

- 추상클래스 자체를 인스턴스화 할 수 없다.  

## 다계층 추상 상속 구조

![[240313_multi_hierarchy_abstract_structure.png]](/02.Dart/_resources/240313_multi_hierarchy_abstract_structure.png)

# 인터페이스

1. 모든 메소드는 추상 메소드여야함  
2. 필드를 가지지 않는다.  

```dart
abstract interface class CleaningService {  
 Shirt washShirt(Shirt shirt);  
 Towel washTowel(Towel towel);  
 Coat washCoat(Coat coat);  
}  
  
class SuwonCleaningService implements CleaningService, Store {  
 @override  
 washCoat(coat) {  
  return coat;  
 }  
  
 @override  
 washShirt(shirt) {  
  return shirt;  
 }  
  
 @override  
 washTowel(towel) {  
  return towel;  
 }  
}
```

`interface` 키워드를 사용하여 일반 `abstract` 클래스와 구분지음  

`interface` 는 `implements` 를 사용하여 자식 클래스에서 상속  

---

> **`interface` 면 모든 메소드를 다 구현해야 하는가?**
>
> `interface` 를 상속하는 클래스가 추상 클래스면 전부 다 구현해야할 필요 없음  
> 일반 클래스일 경우에만 전부 다 구현해야 함  

---

## 인터페이스의 구현 (implements)

`implements` 키워드를 이용하여 인터페이스를 구현함.

```dart
abstract interface class CleaningService {  
 Shirt washShirt(Shirt shirt);  
 Towel washTowel(Towel towel);  
 Coat washCoat(Coat coat);  
}
```

## 인터페이스의 다중구현

여러 인터페이스를 구현하도록 할 수 있다.

```dart
class SuwonCleaningService implements CleaningService, Store
```

> Dart 에서 다중 상속은 할 수 없음  

## 인터페이스의 효과

1. 같은 구현한 클래스들은 공통 메소드를 구현하고 있음을 보장.
2. 어떤 클래스가 인터페이스를 구현하고 있다면, 적어도 그 인터페이스에 정의된 메소드를 가지고 있다는 것이 보증된다.

# implements 와 extends 의 사용방법

```dart
clas Dancer extends Chracter implements Human
```

> extneds 와 implements 를 동시에 사용 할 수 있음

![[240313_implements_extends_usecase.png]](/02.Dart/_resources/240313_implements_extends_usecase.png)

주로 사용할 키워드

- class
- abstract class
- abstract intreface class
