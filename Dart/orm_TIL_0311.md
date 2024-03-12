240311

플러터 과정 6일차


test 코드
-

테스트 코드를 할 때 기본 코드
```dart
import 'package:test/test.dart';

void main() {
  test( 'testCode', () {
    // 여기에 코드를 작성
  });
}
```

test 코드는 given > when > then 기법을 사용한다.
expect() 함수를 활용하여 결과를 검증한다.

## 캡슐화 encapsuation
> 클래스나 인스턴스를 이용하여 현실세계를 객체 지향 프로그램으로 자유롭게 개발 할 수 있게 되었다. 하지만 실수로 속성을 덮어 쓰거나,
잘못된 조작하는 등의 휴먼 에러(human error)를 완전히 없앨 수는 없다. 그래서 dart에 캡슐화라는 것이 있다.
