# 추상클래스
## 상세 정의가 미정인 클래스
- 상속의 재료로 사용됨
```dart
abstract class Character {
  
  //추상 메소드
  void attack(Slime slime);
}
```

## 추상 클래스를 extends를 하면 override 하지않은것이 있다면 메세지 뜸

## 추상클래스는 인스턴스화가 금지되어 있다.

# 인터페이스
1. 모든 메소드는 추상 메소드
2. 필드를 가지지 않음.
```dart
abstract interface class Human {
  void speak();
}

// interface 의 구현
class Student implements Human{
  @override
  void Speak(){
    print('저는 학생이랍니다.');
  }
}
```

- 같은 인터페이스를 구현한 클래스들은 공통 메소드를 구현하고 있음
- 어떤 클래스가 인터페이스를 구현하고 있다면, 적어도 그 인터페이스에 정의된 메소드를 가지고있음이 보증됨.

## 여러 인터페이스를 implements 할 수 있음
## extends 와 implements 를 동시에 사용 가능