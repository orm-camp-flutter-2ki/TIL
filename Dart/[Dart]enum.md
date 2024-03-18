> ### 🙋🏻 enum : 특정 값 집합에 이름을 부여하는 데 사용
ex) 달력에 요일(월~금)과 토요일 :파란색, 일요일 :빨간색 처럼 `값의 집합`을 뜻함

> #### 왜 사용하죠?
1)유형 안정성(Type Safety)<br>
열거형을 사용하면 프로그램의 유형 안전성을 높일 수 있습니다.<br>
2)가독성 향상<br>
열거형은 프로그램의 가독성을 향상시킵니다. 코드를 읽는 사람이 열거형 상수를 보고 해당 값이 무엇을 나타내는지 쉽게 이해할 수 있습니다.<br>
3)제한된 값 집합 표현<br>
열거형은 특정 값 집합에 대한 명확한 정의를 제공합니다. 이는 잘못된 값이 사용되는 것을 방지하고 코드의 예측 가능성을 높입니다.<br>

> _ex) 구구단 만들기_
```dart
enum Operation {
  addition,
  subtraction,
  multiplication,
  division
}
double calculate(Operation operation, double x, double y) {
  switch (operation) {
    case Operation.addition:
      return x + y;
    case Operation.subtraction:
      return x - y;
    case Operation.multiplication:
      return x * y;
    case Operation.division:
      if (y != 0) {
        return x / y;
      } else {
        return double.infinity; // 나누기 0은 무한대로 처리
      }
  }
}
void main() {
  double num1 = 10;
  double num2 = 5;
  // 덧셈 연산
  print("덧셈 결과: ${calculate(Operation.addition, num1, num2)}");
  // 뺄셈 연산
  print("뺄셈 결과: ${calculate(Operation.subtraction, num1, num2)}");
  // 곱셈 연산
  print("곱셈 결과: ${calculate(Operation.multiplication, num1, num2)}");
  // 나눗셈 연산
  print("나눗셈 결과: ${calculate(Operation.division, num1, num2)}");
}
```

> ⭐️ 한장정리!
`enum+switch` 문 조합으로 사용하여, 모든케이스를 강제로 작성해야함!<br>
if문 사용시 enum을 효율적이게 사용하지 않는 방법임으로 비추
