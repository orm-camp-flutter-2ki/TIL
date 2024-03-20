> 함수 (Function):
- 함수는 특정한 기능을 수행하는 코드의 블록이며, 독립적으로 존재할 수 있습니다.
- 함수는 일련의 입력을 받아들이고, 이를 처리하여 결과를 반환할 수 있습니다.
- 함수는 주로 모듈화와 코드 재사용성을 높이기 위해 사용됩니다.<br>
ex) add(a, b) 함수는 두 개의 숫자를 인자로 받아서 그 합을 반환합니다.

> 메서드 (Method):
- 메서드는 객체 지향 프로그래밍에서 객체에 속한 함수를 의미합니다.
- 객체에 의해 호출되며, 해당 객체의 상태를 조작하거나 객체의 기능을 수행합니다.
- 메서드는 객체의 특정 상태에 접근할 수 있고, 객체의 행위를 구현하는 데 사용됩니다.<br>
ex) toString()은 객체의 문자열 표현을 반환하는 메서드이며, 해당 메서드는 특정 객체에 속합니다.

```dart
// 함수 예시
int add(int a, int b) {
  return a + b;
}

void main() {
  int result = add(3, 5); // 함수를 호출하여 결과를 반환
  print('Result of add function: $result');
}

// 메서드 예시
class Calculator {
  int add(int a, int b) { // 객체에 속한 메서드
    return a + b;
  }
}

void main() {
  Calculator calculator = Calculator();
  int result = calculator.add(3, 5); // 객체의 메서드를 호출하여 결과를 반환
  print('Result of add method: $result');
}
```
⭐️정리<br>
`add 함수는 독립적으로 존재`하며, 필요할 때마다 `호출`될 수 있습니다.<br>
반면에 `add 메서드는 Calculator 클래스에 속해` 있으며,<br>
Calculator 객체를 `생성한 후에만 호출`될 수 있습니다.<br>
함수는 객체와 **상관없이 호출**할 수 있지만, 메서드는 ** 특정 객체에 종속** 되어 있습니다.
