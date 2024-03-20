> 🙋🏻1급 객체?
- 변수에 대입 가능한 객체를 1급 객체 (first class object) 라고 한다.<br>
_ex)대표적인 1급 객체 : 값, 인스턴스, 함수_

###  * 함수의 표현 방법

> **기명 함수 (Named Function)**:
가장 일반적인 함수 표현 방법 중 하나입니다. 함수에 이름을 지정하고, 해당 이름을 사용하여 함수를 호출할 수 있습니다.
```dart
int add(int a, int b) {
  return a + b;
}
```

> **익명 함수 (Anonymous Function 또는 람다 함수)**:
함수에 이름을 지정하지 않고 직접 정의하는 방법입니다. 주로 함수를 다른 함수의 인자로 전달하거나 변수에 할당할 때 사용됩니다.
```dart
(int a, int b) {
  return a + b;
}
```

> **화살표 함수 (Arrow Function)**:
주로 간단한 함수를 간결하게 표현할 때 사용됩니다.
```dart
int add(int a, int b) => a + b;
```

> **클로저 (Closure)**:
함수 내부에서 외부 변수에 접근할 수 있는 함수입니다. Dart의 익명 함수는 클로저로 동작합니다.
```dart
int Function(int) makeAdder(int addend) {
  return (int value) => value + addend;
}
```

> **함수형 프로그래밍 특징을 활용한 함수 표현**:<br>
다트는 객체지향 프로그래밍(OOP)과 함수형 프로그래밍(FP) 특징을 모두 제공하는 멀티 패러다임 언어입니다.<br>
함수형 프로그래밍은 자료 처리를 수학적 함수의 계산으로 취급하는 프로그래밍 패러다임이고 `가변 데이터를 멀리하는 특징`을 가집니다<br>

```dart
int Function(int) add(int a) {
  return (int b) => a + b;
}
```
