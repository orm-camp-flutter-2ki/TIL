# 제네릭과 열거형

## 제네릭
```dart
List<E> class
Map<K, V> class
```

- 타입을 바꾸고 싶은 애들을 이렇게 구성하면 나중에 결정이 됨
    - K - key
    - V - Value
    - T - Type
    - E - Elements
    - R - Return

## enum
- 정해 둔 값만 넣어둘 수 있는 타입
    

## 문자열 조작

- string.substring(0,2) →0부터 2까지
- string.replaceAll(LL,XX) →LL을 XX로 바뀜

## 문자열 연결 (String Concatenation)

```dart
dartCopy code
String firstName = 'John';
String lastName = 'Doe';
String fullName = firstName + ' ' + lastName;
print(fullName); // John Doe 출력

```

## 문자열 길이 (String Length)

```dart
dartCopy code
String str = 'Hello, World!';
int length = str.length;
print(length); // 13 출력

```

## 문자열 검색 (String Searching)

```dart
dartCopy code
String str = 'Hello, World!';
bool containsWorld = str.contains('World');
print(containsWorld); // true 출력

```

## 문자열 분할 (String Splitting)

```dart
dartCopy code
String str = 'apple,banana,orange';
List<String> fruits = str.split(',');
print(fruits); // ['apple', 'banana', 'orange'] 출력

```

## 문자열 대/소문자 변환 (String Case Conversion)

```dart
dartCopy code
String str = 'Hello, World!';
String upperCase = str.toUpperCase();
String lowerCase = str.toLowerCase();
print(upperCase); // HELLO, WORLD! 출력
print(lowerCase); // hello, world! 출력

```

## 문자열 치환 (String Replacement)

```dart
dartCopy code
String str = 'Hello, World!';
String newStr = str.replaceAll('World', 'Dart');
print(newStr); // Hello, Dart! 출력

```

## 문자열 자르기 (String Trimming)

```dart
dartCopy code
String str = '   Hello, World!   ';
String trimmedStr = str.trim();
print(trimmedStr); // Hello, World! 출력

```

## StringBuffer
- String은 불변이다.
- 새로운것을 만들어서 new를 하여 만들기 때문에 비용이 많이 든다.
- 그래서 String Buffer을 사용함
