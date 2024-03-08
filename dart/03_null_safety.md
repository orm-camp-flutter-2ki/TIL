# Null-safety
Dart 2.12 버전부터 Null-safety가 도입되었습니다.
2.12 버전이 나온지는 꽤 됐지만 그 전 버전을 쓰던 사람들은 Null-safety에 맞게 마이그레이션을 했어야 했습니다.
Null-safety가 무엇이며 Dart에서 제공되는 Null-safety 관련 키워드는 무엇이 있는지 알아보겠습니다.

### Null? Null-safety?
null은 값이 아예 없는 것을 의미합니다.
0이나 '' 공백같이 빈 값이 아닌 아예 없는 것입니다.
<br>
<img src="https://velog.velcdn.com/images/chojja7188/post/f4cf114e-561b-47e6-a30b-662cb24fc0ab/image.png" width=200>
<br>
Null-safety가 도입되기 전 Dart에서는 String형이나 int형같은 타입에 null을 넣을 수 있었습니다.
그러나 이는 런타임 에러가 발생할 가능성이 컸기에, Dart 2.12 버전 이후로 Null-safety가 도입되고 개편되어 null은 아예 다른 취급을 받게 되었습니다.

```dart
String a = '';
String b = null; // 오류: A value of type 'Null' can't be assigned to a variable of type 'String'.
```
이렇게 Non-Nullable 타입에서는 null이 들어갈 수 없게 되었습니다.
Null-safety가 적용되어 의도치 않은 null로 인한 에러를 사전에 방지할 수 있게 되었습니다.
Null-safety 관련 키워드들을 사용하여 미리 오류를 잡고 안전하게 코딩하는 방법을 알아보겠습니다.

### Nullable type ? (Question Mark)
<br>
<img src="https://velog.velcdn.com/images/chojja7188/post/1b485487-5de4-4ae2-94e6-69e9a9dce12c/image.png" width=200>
<br>
Dart에서는 타입 뒤에 "?" 물음표를 붙여서 null이 들어갈 수 있는 Nullable 타입을 만들 수 있습니다. 물론 타입에 맞는 값을 넣는 것도 가능합니다.
```dart
String a = 'Hello World!';
String b = null; // 이 줄에서만 오류 발생
String? c = 'Hello World!';
String? d = null;
```
이외의 경우가 하나 있는데 Nullable 타입이 아닌 일반 타입에서 null을 직접 넣어주는 것이 아닌 선언만 할 경우에는 컴파일 에러가 발생하지 않습니다.
```dart
String a; // 컴파일 오류가 발생하지 않음
```
다만 출력하거나 계산하기 전에 값이 들어가야 오류없이 정상적인 진행이 가능합니다.

Nullable 타입은 최대한 줄이는 것이 좋습니다.

### ?? 연산자 (Doubue question mark, null aware operator)
"??" 연산자는 왼쪽 값이 null일 경우에 오른쪽 값으로 저장하는 연산자입니다.
```dart
String a = name ?? '홍길동';
// name 변수에 값이 있을 경우에 name의 값으로 저장, 없을 경우 '홍길동'으로 저장
```
위에서 설명한 Nullable 타입을 사용하는 것 대신 "??" 연산자를 사용하는 것이
실수나 오류를 방지하기 좋습니다.
```dart
String? a = name; // 가능하기는 하나 유의해야 함
String b = name ?? ''; // 권장
```

### ?. 연산자 (null aware operator)
"?." 연산자는 Nullable 객체를 안전하게 사용하고자 활용됩니다.
```dart
String? a = null;
print(a.length); // 오류: The property 'length' can't be unconditionally accessed because the receiver can be 'null'.
print(a?.length); // null 출력
```
Nullable 객체의 메소드나 속성을 사용할 때 컴파일 오류 없이 사용할 수 있습니다.

### ! 연산자 (Exclamation mark, null assertion operator)
"!" 연산자는 값이 null이든 null이 아니든 상관하지 않고 값을 강제로 할당하게 합니다.
다만 null이 아님을 개발자가 보증하는 것이므로 신중하게 사용해야 하며,
잘못 사용할 시 런타임 에러가 나타날 수 있습니다.
```dart
String? a = 'Hello World!';
String? b = null;
String a2 = a!;
String b2 = b!; // 오류: Null check operator used on a null value
```

### late 키워드
late 키워드는 값의 초기화를 뒤로 미루고 null을 실수로 사용하는 것을 막아주는 키워드입니다.
late가 앞에 붙은 변수는 지금 당장 값이 할당되지 않더라도 나중에 반드시 할당한다고 약속됩니다.
변수를 선언하는 시점에 값을 넣을 수 없을 때 사용합니다.
```dart
late String a;
a = getValue();
```


### 정리
- Dart는 Null-safety를 지원한다.
- ?, ??, ?., !, late 등으로 null로 인해 찾아오는 오류들을 방지할 수 있다.
- !는 신중하게 사용하자.
