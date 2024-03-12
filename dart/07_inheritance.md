# 상속 (inheritance)
- 이전에 만든 class 와 닮았지만 일부 다른 class 를 만들 필요가 있는 경우
- 복사 붙여넣기를 할 경우
  - 추가 / 수정에 시간이 오래 걸린다.
  - 소스의 파악이나 관리가 어려워진다.

```
class SuperHero extends Hero {
  SuperHero({required super.name, required super.hp});
}
```
- 위와 같이 class명 뒤에 extends <상속하려는 class> 를, 상속자에 this 대신 super 를 붙인다.
- dart 문법에서 다중상속은 금지
- 상속 받으려는 class 에서 named constructor 가 여러개여도 사용하지 않는 constructor까지 전부 상속할 필요는 없다.
```
class Hero {
  Hero({required this.name, required this.hp, this.sword}) {
    print('Hero 클래스의 인스턴스 생성');
  }
}

class SuperHero extends Hero {
  SuperHero({required super.name, required super.hp}) {
    print('SuperHero 클래스의 인스턴스 생성');
  }
}

void main(List<String> arguments) {
  final superHero = SuperHero(name: '한석봉', hp: 50);
}
```

## override
```
class Hero {
  Hero({required this.name, required this.hp, this.sword}) 

  void run() {
    print('$name 뛰는중');
  }
}

class SuperHero extends Hero {
  SuperHero({required super.name, required super.hp});

  @override
  void run() {
    print('$name이 퇴각했다.');
  }
}
```
- 위와 같이 상속받았던 Hero class 의 run() 함수를 재정의 해서 사용할 수 있다.

### 올바른 상속은 `is-a 원칙` 을 따른다.
- SuperHero is a Hero  => O
- Student is a Person  => O
- Sushi is a Food  => O
- Engine is a Car  => X
- Child is a Father  => X
