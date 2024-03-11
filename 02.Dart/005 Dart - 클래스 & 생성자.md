---
title: 005 클래스
author: Kim Donghyeok
created_at: 2024-03-08
updated_at: 2024-03-08
tags:
  - 생존코딩
  - 오름캠프
  - dart
---

# 클래스

## 레퍼런스 타입과 참조

> 레퍼런스 == 참조  

- 가상세계 = 컴퓨터의 메모리 영역
- 인스턴스 = heap 영역안에 확보된 메모

> **Dart 는 모든 타입이 레퍼런스 타입**  

![[ram_program_sturucture.png]](/02.Dart/_resources/ram_program_sturucture.png)

> Dart 에서 문자열 한 글자는 몇 바이트일까?  
>
> C 영문 한자는 1 Byte  한글은 2Byte  
> Java 는 UTF-8 인코딩일 때 1~4 바이트 가변용량

## 클래스의 인스턴스화

클래스의 객체가 생성 될 때 클래스가 인스턴스화 된다. 메모리 heap 영역이 할당 되어 메모리에 저장되게 된다.

```dart
final Hero = Hero(name: '홍길동', hp: 100)
```

![[memory_allocation.png]](/02.Dart/_resources/memory_allocation.png)

> **Dart 는 메모리 영역을 직접 접근하지 않는 언어.**  

---

###### 예제

다음 이미지에서 `hero1` 의 체력은 몇일까?

![[object_reference.png]](/02.Dart/_resources/object_reference.png)

정답은 `200`

*왜?*

`new` 로 인스턴스화 된 객체의 숫자를 세어보면 `hero1` 만 `new` 키워드로 인스턴스 화가 되어있음  (`new` 키워드 생략됨)
`final hero2 = hero1;` 를 해줌으로써 `hero2`는 새로운 객체가 생성되어 인스턴스 화가 된 것이 아님  

> **객체는 메모리의 Stack 영역에, 인스턴스는 메모리의 Heap 영역에 할당.**  

---

##### 실습

`Sword` 클래스를 작성해보자

- Sword 클래스는 생성자에 required 키워드를 사용하여 작성

`Wizard` 클래스를 작성 해보자

- Wizard 클래스는 생성자에 required 키워드를 사용하여 작성
- `Hero` 클래스를 인자로 받아 해당 객체의 hp를 10 회복 시키는 메소드를 작성

---

> **Dart 에서는 모든 타입이 레퍼런스 타입**
>
> int 형이나 double 형 같은 기본형 (primitive type) 뿐만 아니라 String 도 Hero 와 같은 ***"레퍼런스 타입"***

---

## 생성자 (constructor)

인스턴스를 생성하는 방법을 제공

```dart
class Wizard {
 String name;
 int hp;
 
 Wizard(this.name, this.hp);
}
```

모든 클래스는 반드시 1개 이상의 생성자를 가진다

```dart
class Person {  
// 생성자를 작성하지 않아도 기본 생성자는 있다고 본다.  
// Person();  
}
```

### named parameter

생성자에 `{}` 를 사용하면 named parameter 임

데이터 타입이 null 을 허용하지 않으면 `required` 를 붙여야 함

```dart
class Hero {  
 String name;  
 int hp;  
 Sword? sword;
   
 Hero({  
  required this.name,  
  required this.hp,  
  this.sword  
 });
}
```

## 필수 파라미터와 named parameter

필수 parameter 와 optional parameter 를 동시에 사용할 수 있다.

```dart
class Hero {  
 String name;  
 int hp;  
 Sword? sword; // nullable  

 // 필수 parameter 와 optional parameter 를 동시에 사용할 수 있다.
 Hero(this.name, this.hp, {this.sword});  
});
```

필수 parameter 와 named parameter 를 동시에 사용 할 경우 필수 parameter 가 앞에 와야 함 마지막 파라미터 뒤에 콤마를 찍을 수 없음

```dart
final hero1 = Hero('전사', 50);
final hero1 = Hero('검사', 100, sword: sword);
```

## 기본 값 지정

```dart
class Person {  
 String name;  
 int age;  
 Car? car;  

 // default 값 지정
 Person({this.name = '홍길동', this.age = 20, this.car});  
}
```

## 생성자의 오버로드

아래 클래스의 생성자는 몇개의 생성자가 가능할까?

```dart
class Person {  
 String name;  
 int age;  
 Car? car;  
   
 Person({this.name = '홍길동', this.age = 20, this.car});  
}
```

정답은 8개

```dart
void main() {
 // Person 의 생성자는 몇개가 가능할까? -> 8개  
 final person1 = Person(name: '홍길동', age: 20, car: car);  
 final person2 = Person(name: '홍길동', age: 20);  
 final person3 = Person(name: '홍길동', car: car);  
 final person4 = Person(age: 20, car: car);  
 final person5 = Person(name: '홍길동');  
 final person6 = Person(age: 20);  
 final person7 = Person(car: car);  
 final person8 = Person();
}
```

- Person 클래스의 필드는 name, age 필수이고, car 필드가 nullable 이다  
- Person의 생성자에서 모든 인자는 named parameter 로 되어있음  
- name, age 필드는 필수이지만 생성자에서 기본값이 할당되어있기 때문에 생성자에서 값이 없어도 됨  
- car 필드는 nullable 이기 때문에 생성자에서 값이 없어도 됨  
- 따라서, 3개 필드에 대해서 나올수 있는 생성자 경우의 수는 2^3 = 8개

## 정적 필드와 정적 메소드 (static)

### 정적 필드

같은 클래스에서 작성해도, 각각의 인스턴스에서 별도의 필드를 가짐

```dart
class Hero {
 int money = 100;
 String name;
 int hp;
 Sword? sword;
}
```

static 키워드를 사용해 필드를 공유

```dart
class Hero {
 static int money = 100;
 String name;
 int hp;
 Sword? sword;
}
```

정적필드에 접근

```dart
void main() {
 final hero = Hero(name: '홍길동', hp: 100);
 print(Hero.money)
}
```

static 키워드로 정의한 변수는 인스턴스가 생성되어있지 않아도 접근 가능

```dart
void main() {
 print(Hero.money); 
}
```

### 정적 메소드

```dart
class Hero {
 static int money = 100;
 String name;
 int hp;
 Sword? sword;

 static void setRandomMoney() {
  money = Random.nextInt(1000);
 }
}
```

정적 메소드의  호출

```dart
void main() {
 Hero.setRandomMoney();
 print(Hero.money);
 
 final hero = Hero(name: '홍길동', hp: 100);
 print(Hero.money)
}
```

정적 메소드 안에서 엑세스 할수 있는 것은 정적 멤버만 가능

```dart
class Hero {
 static int money = 100;
 String name;
 int hp;
 Sword? sword;

 static void setRandomMoney() {
  money = Random.nextInt(1000);
  print('$name 의 소지금을 추가했다.); // 접근불가
 }
}
```

---

# 정리

레퍼런스 타입의 참조

- 레퍼런스 타입변수의 안에는 "인스턴스의 정보가 담겨있는 메모리 주소" 가 들어있다.
- 어떤 레퍼런스 타입 변수를 다른 변수에 대입하면, 주소만 복사 된다.
- 레퍼런스 타입은 필드나 메소드의 인수, 리턴 값의 타입으로도 사용된다.

생성자

- "클래스 명과 동일 명칭으로, 리턴값의 타입이 명시되어 있지 않은 메소드"는 생성자로 사용된다.
- 생성자는 `new`에 의한 인스턴스화의 직후에 자동적으로 실행된다. Dart 에서 `new` 는 생략 가능
- 생성자는 오버로드에 의한 복수 정의가 된다.
- 클래스에 생성자 정의가 1개도 없는 경우에 한해, 컴파일러가의 기본 생성자를 자동으로 정의 해준다.
정적멤버
- static 키워드가 붙어있는 정적멤버(필드 또는 메소드)

 1. 각 인스턴스가 아닌, 클래스에 실체가 준비된다.
 2. 인스턴스를 1개도 생성하지 않아도 이용가능

- 정적 메소드는 그 내부에 정적이지 않은 메소드나 필드를 시용하는 것이 불가능하다

---

# 연습문제

Cleric 클래스에 관하여 2가지 수정

1. Cleric 클래스의 **최대 HP, 최대 MP의 필드가 공유 되도록  필드 선언에 적절한 키워드를 추가**
2. 아래의 방침에 따라 생성자를 추가
1. 이 클래스는 Cleric(“아서스", hp: 40, mp: 5) 와 같이, 이름, HP, MP 를 지정하여 인스턴스화 할 수 있다
2. 이 클래스는 Cleric(“아서스", hp: 35) 와 같이, 이름과 HP만으로 지정하여 인스턴스화 할 수 있다. 이 때, MP는 최대 MP와 같은 값이 초기화 된다
3. 이 클래스는 Cleric(“아서스") 와 같이 이름만을 지정하여 인스턴스화 할 수 있다. 이 때, HP 와 MP 는 최대 HP와 최대 MP로 초기화 된다
4. 이 클래스는 Cleric() 과 같이 이름을 지정하지 않는 경우에는 인스턴스화 할 수 없다고 한다. (이름이 없는 성직자는 존재 할 수 없음)
5. 생성자는 가능한 한 중복되는 코드가 없도록 작성한다

---

# static final, static const

`const` 로 선언된 상수는 컴파일 단계에서 값이 결정  
`final` 로 선언된 상수는 런타임에서 사용될 때 값이 결정  

`static` 키워드는 공용자원으로 런타임 전에 값이 결정되어 메모리에 할당된다.

```dart
class Cleric {  
 static const int maxHp = 50;  
 static const int maxMp = 10;  
 // static final int maxHp = 50; // 생성자에서 사용 불가능  
 // static final int maxMp = 10; // 생성자에서 사용 불가능
   
 String name;  
 int hp;  
 int mp;  
   
 Cleric(this.name, {this.hp = maxHp, this.mp = maxMp});
}
```

**생성자는 생성자가 호출 될 때 컴파일 단계에서 이미 결정된 값만 사용이 가능하다.**

따라서, 객체가 생성자를 호출하여 인스턴스화 할 때 사용하는 값이  `static` 으로 선언 되었다고 해도
`final` 로 선언된 상수는 아직 값이 결정되지 않아 생성자에서 사용할 수 없지만  
`const` 로 선언된 상수는 컴파일 단계에서 값이 결정되었기 때문에 생성자에서 사용이 가능하다.
