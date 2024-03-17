# var, dynamic, object
Dart에서 모든 타입으로 초기화할 수 있는 var와 dynamic과 Object(Object?)를 각각 어떻게 쓰고
무슨 차이가 있는지에 대해서 알아보겠습니다.

### var
var는 변수를 선언해주는 키워드입니다.
몇몇 다른 언어의 var는 한 번 지정해도 아무 값이나 계속 넣을 수 있지만
Dart에서는 한 번 초기화를 했을 때의 타입을 그대로 따라갑니다.

**JavaScript**
```js
var a = 1;
a = 'Hello World!';
a = 3.2;
// 정상 작동
```
**Dart**
```dart
var a = 1; // a 변수는 int 타입으로 할당
a = 'Hello World!';
// 오류: A value of type 'String' can't be assigned to a variable of type 'int'. 
a = 3.2;
// 오류: A value of type 'double' can't be assigned to a variable of type 'int'.
```
만약 처음 선언할 때 초기화를 시켜주지 않으면 dynamic 타입으로 설정됩니다.
```dart
var a; // dynamic 타입
a = 2;
a = 2.5;
// 정상 작동
```
### dynamic
dynamic은 Dart의 타입 중 하나입니다.
어떤 값을 넣어도 컴파일이 가능합니다.
```dart
dynamic a = 1;
a = 'Hi';
a = 3.14;
a = null;
// 정상 작동
```
다만 어떤 값을 넣어도 컴파일이 가능한만큼 잘못 사용하면 런타임 에러가 발생할 수도 있습니다.
```dart
dynamic a = '1';
int b = a + 3;
// 런타임 오류: type 'int' is not a subtype of type 'String' of 'other'
```
심지어는 없는 메소드와 프로퍼티를 사용해도 컴파일이 됩니다.
```dart
dynamic a = 1;
a.fakeMethod(); // 런타임 오류
print(a.fakeProperty); // 런타임 오류
```
따라서 dynamic을 무분별하게 사용하면 오류가 발생할 가능성이 있기 때문에
Map<String, dynamic>과 같이 특수한 상황을 제외하고는
사용을 지양해야 합니다.

### Object, Object?
Dart에서는 모든 것이 객체입니다.
따라서 모든 클래스가 Object 클래스를 상속하고 있습니다.
Nullable 클래스는 Object? 클래스를 상속합니다.
```dart
Object a = 1;
a = 'Hi';
a = 3.14;

Object? b = 1;
b = null;
```
타입에 대한 검사가 있기 때문에 dynamic보다는 Object/Object?를 활용하는게 적절할 수 있겠습니다.

### 정리
- var는 처음 할당된 값의 타입을 따라감
- dynamic은 모든 값이 들어올 수 있음
- Object는 Non-nullable의 최상위, Object?는 Nullable의 최상위 타입
- dynamic은 런타임 오류를 발생시킬 수 있으므로 사용에 유의

자료 :
https://dart.dev/language/type-system
https://dart.dev/language/variables
