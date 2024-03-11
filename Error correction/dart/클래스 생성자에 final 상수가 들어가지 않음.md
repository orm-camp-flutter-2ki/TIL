### 📄오류 발생

```dart
class Cleric {

  static final int maxHp = 50;

  static final int maxMp = 10;

  String name;

  int mp;

  int hp;

  Cleric(this.name, {this.hp = Cleric.maxHp, this.mp = Cleric.maxMp});

  void selfAid() {

    if (mp >= 5) {

      mp -= 5;

      hp = Cleric.maxHp;

    }

  }

  int pray(int time) {

    // print('기도 시간을 입력하시오.');

    // int time = int.parse(stdin.readLineSync()!);

    int prayMp = Random().nextInt(3) + time;

    mp = prayMp + mp;

    mp = mp >= 10 ? 10 : mp;

    return prayMp;

  }

}
```

- The default value of an optional parameter must be constant. 오류 발생

### 📄 원인

- final로 상수를 선언하면 런타임시에 읽혀서 상수로 취급되지 않음


### 📄 해결 방법

- const로 상수를 선언하면 컴파일 타임에 읽혀 상수로 취급됨
