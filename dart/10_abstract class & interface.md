## 추상클래스 Abstract
> 추상메서드(abstract method)를 하나라도 포함하고있다면 추상클래스(abstract class)이다.
- 추상 메소드는 선언부만이 존재하며, 구현부는 작성되어 있지 않다.
  ex) `int getInt();`
- 작성되어 있지 않은 구현부는 자식 클래스에서 오버라이딩(`@override`)하여 사용하는 것이다.

```dart
abstract class Character{
  String name;
  int hp;

  //선언부만 존재
  void attack(Slime slime); 
}

class Hero extends Character{
  Hero(super.name, super.hp);
}

//override하여 구현부 작성
@override               
void attack(Slime slime){
  print('$name이 $slime을 공격했다.);
  slime.hp -= 10;
}
```

### 추상클래스를 쓰는 이유
- 미정인 기능들을 우려하여 추상화 클래스와 추상화메서드를 활용하여 부모클래스를 개발하면, 예기치 않은 인스턴스화나 오버라이드의 미구현의 걱정이 없다
<br/>
<br/>

## 인터페이스 Interface
> 추상 클래스 중에, 기본적으로 추상메소드만 가지고 있는 것을 '인터페이스' 로서 특별 취급 한다.
- 인터페이스를 부모로 두는 자식 클래스 정의에 implements 를 사용
- 복수의 인터페이스를 부모로 두는 다중상속 효과가 가능.

```dart
abstract interface class Thing {
  double get weight;
  
  int modelYear();
}

//modelYear 추상메서드가 구현되지 않았기 때문에 abstract class로 남게 된다.
abstract class TangibleAsset extends Asset implements Thing {
  double _weight;
  
  @override
  double get weight => _weight;

  TangibleAsset({required super.name, required double weight})
      : _weight = weight;
}
```
### 인터페이스를 쓰는 이유
- 상속(Inheritance)은 한번만 받을 수 있기 때문에, 그 외의 공통적인 기능은 인터페이스를 활용하여 생성한다.(이후 implements로 오버라이드 한다.)
