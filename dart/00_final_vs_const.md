# final vs const

> final 키워드와 const 키워드

## 공통점
- 상수 키워드라는 공통점이 있다.
#### final
```dart
final int a = 10;
a = 5; // 오류: The final variable 'a' can only be set once.
```
#### const

```dart
const int b = 10;
b = 5; // 오류: Constant variables can't be assigned a value.
```

## 차이점
> **final은 런타임 시점에 값이 할당되어 상수가 되고,
const는 컴파일 시점에 값이 할당되어 상수가 된다.**

컴파일이 된 후에 런타임 상태가 되므로,
const는 프로그램이 실행되기 전에 컴파일하는 과정에서 할당이 되는데
이 때문에 차이가 생긴다.

#### final
```dart
final a = DateTime.now();
print(a);
> 2024-03-05 19:27:27.106124
```
#### const
```dart
const b = DateTime.now();
// 오류: Const variables must be initialized with a constant value
```
DateTime.now()는 코드가 실행될 때의 시간을 반환.
final의 경우에는 코드가 실행되는 런타임 시점 동안에 할당이 되는 반면
const는 그 전에 할당을 받아야하기 때문에 오류가 발생.
따라서 const는 프로그램을 실행하기 전에 값이 할당되어 있어야 정상적으로 사용 가능.

생성자의 경우에서도 차이점이 있음.
#### final
```dart
class Warrior() {
  static final int maxHp = 100;
  String name;
  String hp;
  
  Warrior(this.name, this.hp = maxHp);
  // 오류: The default value of an optional parameter must be constant
}
```
#### const
```dart
class Warrior() {
  static const int maxHp = 100;
  String name;
  String hp;
  
  Warrior(this.name, this.hp = maxHp);
}
```
static과 생성자는 런타임 전에 값이 결정되어야 하기 때문에
런타임 시점에 할당되는 final은 이 경우에 사용할 수 없음.
따라서 이런 상황에서는 const를 사용.

또한 처음 상수를 선언할 때에도 다른 부분이 있다.

#### final
```dart
final int a;
final int a = 1;
```
#### const
```dart
const int b;
const int b = 1;
// 오류: The constant 'b' must be initialized.
```
final의 경우 선언하면서 값을 할당하지 않아도 나중에 1번 할당이 가능하지만
const는 선언하면서 바로 할당을 해줘야 한다.
