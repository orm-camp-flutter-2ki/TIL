## 📖 열거형(enum)
<br>

- 정해둔 값만 넣을 수 있는 타입
- static으로 활용 가능

```dart
enum KeyType {

  padlock,

  buttom,

  dial,

  finger;

  int get value {

    switch (this) {

      case KeyType.padlock:

        return 1024;

      case KeyType.buttom:

        return 10000;

      case KeyType.dial:

        return 30000;

      case KeyType.finger:

        return 1000000;

    }

  }

}
```
- switch와의 조합으로 모든 케이스를 강제로 작성해야 함
<br>
<br>
