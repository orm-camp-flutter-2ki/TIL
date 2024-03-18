# 캡슐화 (encapsulation)

### 휴먼에러를 방지하기 위함.

### 오타와 같은 휴먼 에러가 있을경우?

```

class Inn {
    void checkIn(Hero hero){
    // 여기는 여관인가 무덤인가
    hero.hp -= 100;
    }
}
```

### 멤버에 대한 액세스 제어

- 접근 지정자
    - private : 멤버 앞에 '_' 붙이기
      이럴 경우, 자기 자신의 클래스 안에서만 접근이 가능함.

```
class Hero {
// static 변수는 클래스의 모든 인스턴스가 공유하는 변수. 변화가 생기면 모든 객체에 반영됨.
    static int money = 100;
    String name;
// _hp는 Hero 클래스 내부에서만 접근할 수 있고, 외부에서는 접근할 수 없음
    int _hp;
// 생성자의 매개변수로 받은 hp를 private 변수인 _hp에 할당하고있음.   
    Hero({
      required this.name,
      required int hp,
      this.sword,
      }) : _hp = hp;

```

### 메소드를 private 으로 지정 할 수도 있다.

### getter & setter

객체의 필드에 접근하기 위한 특별한 메서드.

- getter : 읽기 전용 프로퍼티
- setter : 쓰기 전용 프로퍼티

쓰는 이유? 값의 타당성을 검사할 수 있음.

```dart

String _name;

set name(String value) {
  if (value.length <= 1) =>
  throw Exception('이름이 너무 짧습니다');
  _name = value;
}

String get name => _name;
```

### 클래스에 대한 엑세스 제어

```dart
class _B {}
```


# 컬렉션(자료구조)
- List : 순서대로 쌓여있는 구조, 중복허용
- Map : key, value 쌍으로 저장, 중복 불가
- set : 순서가 없는 집합, 중복 불가

dart에는 배열이 없고 list만 있음. 크기를 정해두지 않고 요소를 추가할때마다 크기가 커짐
