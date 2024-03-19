240318 (Mon)

플러터 과정 11일차

 제네릭 
 =
객체 지향에서 지원하는 것
List<E> class & Map<K, V> class

<> 안을 제네릭이라고 부른다.

타입을 나중에 원하는 형태로 정의할 수있음

타입 안전 (type safe) 효과

### 제네릭을 사용하지 않는 Pocket 클래스(ver 1)
```dart
class Pocket {
Object? _data;

void put(Object data) {
_data = data;

}

Object? get() {
return _data;

}
}
```

### 제네릭을 사용한 Pocket 클래스 (ver 2)
```dart
class Pocket<E> {
E? _data;

void put(E data) {
data = data;

E? get() {
return _data;

}
}
```

### 타입에 제약을 추가한 Pocket 클래스 (ver 3)
```dart
class Pocket<E extends book> {
E? _data;

void put(E data) {
data = data;

E? get() {
return _data;

}

}
```

## 열거형
정해둔 값만 넣어 놓을 수 있는 타입
```dart
void main(){
AuthState state = AuthState.authenticated;

switch (authState) {
case AuthState. authenticated:
print('authenticated');
break;
case AuthState. unauthenticated:
print('unauthenticated');
break;
case AuthState. unknown:
print('unknown');
break;

}

}
enum AuthState{
	authenticated,	unauthenticated, unknown
}
```
 문자열 정리
=

### 문자열 처리 (결합)

'Hello' + ' Dart'
=> 'Hello Dart'

***
### 수식을 활용한 문자열 결합

String
'${3 +2}' => 5
'${"word".toUpperCase()}' =>WORD
'myObject' => the value of myObject.toString()

***
### 문자열 처리 (일부 떼어네기)

'HELLO'
=> 'HE'

const string = 'HELLO';
print(string.substring(0 , 2);

***
### 문자열 처리 (일부 치환)

'HELLO'
=> 'HEXXO'

const sting = 'HELLO';
print(string.replaceAll('LL', 'XX'));

***
### 문자열 처리 (분리)

'1,2,3'
=> '1', '2', '3'

final string = '1,2,3';
final splited = string.split(',');
splited.forEach((e) {
  print(e);
  });

***
### 문자열 처리 (대소문자 변경)

###### 'HELLO'
###### => 'hello'

final string = 'HELLO';
//소문자 변경
print(string.toLowerCase());
//대문자 변경
print(string.toUpperCase());

***
### 문자열 처리 (검색)

'Dart and Flutter'
=> D는 1번째 글자

final string = 'Dart and Flutter';

print(string.indexOf('D')); //0 단어가 몇 번째에 있는지
print(string.contains('Flutter')); //true 포함 관계
print(string.endsWith('Flutter')); //true 끝나는 단어가 맞는지
print(string.lastIndexOf('t')); // 13 뒤에서 몇번째에 단어가 있는지

***
### 문자열 처리 (내용비교)

final s1 = 'Dart';
final s2 = 'dart';

print(s1 == s2); // false
print(s1.toLowerCase() == s2.toLowerCase()); // true

***
### 문자열 처리 (길이)

final s1 = 'Dart';

print(s1.length); // 4  길이
print(s1.isEmpthy); // false  길이가 0인

***
### 문자열 처리 (변환)
final s1 = 'Dart and Flutter';

print(s1. toLowerCase()); // 소문자로
print (s1.toUpperCase()); // 대문자로
print(s1.trim()); // 좌우 공백 제거
print(s1. replaceAll('and', 'or')); // 교체체

***
문자열(String) 관련 생각할 점
-
```dart
void main() {
String string = 'Dart is fun';

string = 'hello';
}
```
위의 코드를 보면 string 변수의 타입을 String으로 선언 뒤에 string의 입력값을 'hello'로 바꾸었다.
이때 'Dart is fun'이라는 문장은 사라지는 가?
답은 '아니다' String 타입은 불변하는 타입이기 때문에 string에 대입하는 값이 달라진 것이지 원래의 문장은 사라지지 않고 메모리에 남아있는다. 하지만 나중에 가비지 컬랙터가 사용하지 않는 메모리를 최적하기 위해 정리한다.
String 타입이 느린 이유도 이와 같이 기존에 문자열을 추가하는 것이 아닌 new 생성자로 계속 계속 새롭게 만드는 거이기 때문이다.
