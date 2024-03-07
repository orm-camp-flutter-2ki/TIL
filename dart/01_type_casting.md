# Type casting

> 타입 캐스팅, 형변환

### 자동 형변환?
Dart에서는 자동 형변환이 되지 않는다.
자동 형변환이란 작은 타입이 큰 타입으로 이동될 때 큰 타입에 맞게 자동적으로 형변환이 되는 것을 말하는데,
JAVA와 같은 언어에서는 자동 형변환이 가능하지만 Dart에서는 불가능하다.
#### JAVA
```java
int a = 1;
double b = a;
```
#### Dart
```dart
int a = 1;
double b = a;
// 오류: A value of type 'int' can't be assigned to a variable of type 'double'.

```

## to 메소드
- 앞에 to~가 붙는 메소드.
- 대표적으로 toString(), toInt(), toDouble()가 있으며, to 뒤에 붙은 타입으로 변환 가능.
```dart
int a = 10; // int형 a 선언
double b = a.toDouble(); // int형 a의 값을 double형 b에 저장
String c = b.toString(); // double형 b의 값을 String형 c에 저장
```
## parse 메소드
- 타입.parse('문자열') 형태로 사용.
- int.parse(a), double.parse(a), Uri.parse(a)와 같이 사용.
- parse의 인자로 문자열이 들어가야 하기 때문에 문자 데이터를 변환해야 할 때 유용.
```dart
String value = '1234';
int number = int.parse(value); // String형 '1234'를 int형 1234로 저장
```

## as 연산자
- 뒤에 as int, as double 과 같은 형식으로 붙여서 형변환이 가능.
- 형변환에 맞지 않은 값을 넣어도 타입만 같으면 컴파일 에러가 발생하지 않음.
- 잘못 사용할 시 런타임 에러 발생하므로 유의.
```dart
int a = 1;
double b = a as double;
```

```dart
String a = 'Hello World!';
double b = a as double;
// 런타임 오류, type 'String' is not a subtype of type 'double' in type cast
```
