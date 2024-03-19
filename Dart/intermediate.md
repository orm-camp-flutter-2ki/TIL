# [Dart 중급]

---

### <Dart 테스트코드 작성>
  1. 테스트하고자 하는 파일을 고른다 (lib/파일명.dart)
  2. test 디렉토리 아래 동일 위치에 _test를 붙인 파일을 작성한다. (test/파일명_test.dart)
     - 파일명_test.dart 파일에서 아래의 패키지를 import한다.
     ```dart
     import 'package:test/test.dart'; // equals(), expect(), test(), group() 함수 사용
     ```
  3. 여러가지 테스트 기법 중 given > when > then 기법을 사용한다.
     ```dart
     void main() {
       test('테스트명', () {
       // given(준비)
       final wizard = Wizard(name: '마법사', hp : 100);
       final hero = Hero(name: '히어로', hp: 10);
       // when(실행)
       wizard.heal(hero);
       // then(검증)
       expect(hero.hp, equals(20));
     });
     }
     ```
     - given : 테스트 대상 자료가 주어지고
     - when : 테스트 대상 자료에 메소드가 실행되고
     - then : 메소드가 실행된 이후, 테스트 대상 자료가 원하는 결과가 같은지 확인
       - ```expect()``` 함수 사용, ```expect(a, equals(b))``` a 결과와 b를 비교 (같으면 테스트 통과, 아니면 실패)

---

### <인스턴스의 기본 조작>
- Object Class
  - 모든 클래스는 Object 클래스의 메서드와 프로퍼티를 가지고 있다
  - Object 타입 변수에는 모든 인스턴스를 대입할 수 있다
  - **Object 클래스의 대표 메서드 및 프로퍼티** (오버라이드 하여, 원하는 결과를 얻도록 수정할 수 있음)
    - toString() : 문자열 표현을 얻음
    - operator == : 비교 
    - hashCode : 해시값을 얻음
  - ==와 같은 연산자를 @overide 하여 사용하기 위해서는 [**Comparable 인터페이스**](https://api.flutter.dev/flutter/dart-core/Comparable-class.html)를 구현해야 한다.
    - implements Comparable
      ```dart
      // class Book -> class Book implements Comparable<Book> 
      class Book implements Comparable<Book> {
        String title;
      
        DateTime publishDate;
        String comment;
      
        Book({
          required this.title,
          required this.comment,
          DateTime? publishDate,
        }) : publishDate = publishDate ?? DateTime.now();
      
        String _getFormattedDate(DateTime dateTime) {
          return '${dateTime.year}-${dateTime.month}-${dateTime.day}';
        }
      
        @override
        bool operator ==(Object other) =>
            identical(this, other) ||
            other is Book &&
                runtimeType == other.runtimeType &&
                title == other.title &&
                publishDate.year == other.publishDate.year &&
                publishDate.month == other.publishDate.month &&
                publishDate.day == other.publishDate.day;
      
        @override
        int get hashCode =>
            title.hashCode ^ publishDate.year ^ publishDate.month ^ publishDate.day;
      
        @override
        int compareTo(Book other) {
          return publishDate.compareTo(other.publishDate);
        }
      
        Book copyWith({
          String? title,
          DateTime? publishDate,
          String? comment,
        }) {
          return Book(
            title: title ?? this.title,
            publishDate: publishDate ?? this.publishDate,
            comment: comment ?? this.comment,
          );
        }
      }     
      ```
  
- 얕은 복사(기존 참조값을 공유하여 값 복사) : ```=``` 연산자로 인스턴스 바로 복사
- 깊은 복사(새로운 참조값에 값 복사) : ```copyWith()``` 과 같은 메소드를 작성하여 사용 *(Dart는 깊은복사를 기본 메소드로 제공하지 않음)*
  ```dart
  void main() {
    Book book = Book(title: '플러터', comment:'원본');

    Book book2 = book; // 얕은 복사(shallow copy)
    print(book == book2); // true
  
    Book book3 = book.copyWith(); // 깊은 복사(deep copy)
    print(book == book3); // 동등성 규칙 Overide 하지 않을 시 false
  }
  ```
  
---

### <제네릭, 열거형>
 - **제네릭** : ```< >``` 괄호 안에 특정 데이터 타입 지정 (타입을 나중에 원하는 형태로 정의할 수 있음)
   - 용례 : 클래스가 다루는 데이터 타입이 많은 경우에 개발을 용이하게, 타입 안전 효과
   ```dart
   class List <E>
   class HashSet<E> {}
   class Map<K,V> {}

   abstract class ExpressionVisitor<R> {
    R visitBinary(BinaryExpression node);
    R visitLiteral(LiteralExpression node);
    R visitUnary(UnaryExpression node);
    }
   ```
   - E : 컬렉션의 **요소** 유형
   - K, V : 연관 컬렉션의 **키 및 값** 유형
   - R : **함수 또는 클래스의 메서드의 반환** 유형
   
 - **열거형** : **정해둔 값만 넣어둘 수 있는 타입** (예 : 인증상태), **switch문과의 조합으로 모든 케이스를 강제로 작성해야 함**
   ```dart
   enum AuthState {
     authenticated,
     unauthenticated,
     unknown,
   }
   ```

   ```dart
    void main() {
      AuthState authState = AuthState.authenticated; // 예시로 authenticated로 설정
    
      switch (authState) {
        case AuthState.authenticated:
          print('authenticated'); // 출력
          break;
        case AuthState.unauthenticated:
          print('unauthenticated');
          break;
        case AuthState.unknown:
          print('unknown');
          break;
        default:
          print('Invalid state');
      }
    }
   ```
   
---

### <문자열 조작>
- ${수식}을 활용한 문자열 결합
  ```dart
  '${3+2}' // 5
  '${"word".toUpperCase()}' // 'WORD'
  '$myObject // The Value of myObject.toString()
  ```

- 문자열 일부 떼어내기(Substring)
  ```dart
  const string = 'HELLO';
  print(string.substring(0, 2)); // 'HE'
  ```

- 문자열 일부 치환
  ```dart
  const string = 'HELLO';
  print(string.replaceALL('LL', 'R'));; // 'HERO'
  ```

- 문자열 분리
  ```dart
  final string = '1,2,3';
  final splited = string.split(',');

  splited.forEach((e) {
    print(e);
  });
  ```

- 대소문자 변경
  ```dart
  final string = 'HELLO';
  print(string.toLowerCase()); // 'hello'
  ```

- 검색
  ```dart
  final string = 'HELLO';
  print(string.indexOf('E')); // 2
  ```

- 내용 비교
  ```dart
  final s1 = 'Dart';
  final s2 = 'dart';
  print(s1 == s2); // false
  print(s1.toLowerCase() == s2.toLowerCAse()); // true
  ```

- 길이
  ```dart
  final s1 = 'Dart';

  print(s1.length); // 4
  print(s1.isEmpty); // false (길이가 0이 아니면 false, 길이가 0이면 true)
  ```

- 검색
  ```dart
  final s1 = 'Dart and Flutter';
  print(s1.contains('Flutter')); // true
  print(s1.endsWith('Flutter')); // true
  print(s1.indexOf('Dart')); // 0
  print(s1.lastIndexOf('t')); // 13 (뒤에서 몇번째에 단어가 있는지)
  ```

- 변환
  ```
  final s1 = 'Dart and Flutter';

  print(s1.toLowerCase()); // 소문자로
  print(s1.toUpperrCase()); // 대문자로
  print(s1.trim()); // 좌우 공백 제거
  print(s1.replaceAll('and', 'or)); // 교체
  ```

- StringBuffer을 이용한 문자열 결합 : ```+``` 연산자를 이용할 때 보다 매우 빠르다.
  - ```+``` 연산자가 느린 이유 : String 인스턴스는 불변 객체로, 결합하려는 문자마다 각각 메모리 생성해야하는 문제가 있다. 
  ```dart
  final buffer = StringBuffer('Dart');

  buffer
    ..write(' and ')
    ..write('Flutter');

  print(buffer.toString()); // Dart and Flutter
  ```
  - ```write()```메서드로 결합한 결과를 내부 메모리(버퍼)에 담아두고 toString()으로 결과를 얻음. 
  - ```..```(cascade) 연산자 : void 리턴인 함수의 앞에 사용하면 해당 객체의 레퍼런스를 반환하여 메서드 체인을 사용할 수 있음.
 
    
---

### <예외처리>
- 개념 : 프로그램을 설계할 때 **실행 시 예외 사항이 발생할 가능성이 있는 것을 예측**하여, **사전에 예외처리**가 되도록 함
  - **에러가 발생했을 때 프로그램이 중단 되는 것을 방지하기 위함** (하지 않으면, 에러가 났을 때 프로그램이 중단됨)
    
- 에러의 종류
  1. 문법 에러(Syntax Error) : 코드의 형식적 오류
     - 디버깅 방법 : 컴파일러의 지적을 보고 수정
  2. 논리 에러 (Logic Error) : 기술한 처리 내용에 논리적인 오류가 있음
     - 디버깅 방법 : 원인을 스스로 찾아서 해결해야 함
  3. 실행 시 에러 (Runtime Error) : 실행 중 **예외적인 상황**이 발생하여 동작이 중지됨
     - 디버깅 방법 : *예외*

- **예외적인 상황**
  - 메모리 부족
  - 파일을 찾을 수 없음
  - 네트워크 통신 불가

- 예외처리
  - **try-catch문을 사용하면, try 블록 내에 예외(런타임 에러)가 발생했을 때 catch 블록에서 처리가 옮겨진다**
    ```dart
    void main() {
      final numString = '10.5';
      late int num;
    
      try {
        num = int.parse(numString);
      } catch (error) {
        num = 0; // 예외가 발생하면 0으로 처리
      }
    
      print(num);
    }
    ```
  - finally 블록으로 나중에 꼭 해야하는 처리를 할 수 있다(예외 발생 여부에 관계없이 일부 코드가 실행되도록)
    - ```try {}, on ErrorType{ }, catch(error){ }, finally {}``` 형태
      - try{ }에서 에러가 나면, 예측한 on ErrorType 인 경우 { }을 실행
      - try{ }에서 에러가 나면, 예측 불가능한 ErrorType인 경우 catch { }을 실행
      - 에러발생에 상관없이, finally {} 실행
  - throw 문을 사용하면 임의로 예외를 발생시킬 수 있다.
    
--- 

### <파일 조작>
- 파일 조작의 기본 순서
  1. 파일을 연다
  2. 파일을 읽거나 쓴다
  3. 파일을 닫는다

  ```dart
  import 'dart:io';

  // 1. 파일 열기
  String source = 'path/source.txt'
  final file = File(source);
  
  // 2-1. 파일 읽기
  final content = file.readAsStringSync();
  print('File Content: $content');
  
  // 2-2. 파일 쓰기
  final outputFile = File('path/target.txt'); // 출력 파일 경로 지정
  outputFile.writeAsStringSync(content);
  
  // 3. 파일 닫기 (Dart에서는 파일을 자동으로 관리하므로 개발자가 파일을 직접 닫을 필요가 없다.)
  ```
  
--- 

### <데이터 형식>
1. CSV(comma-separated values) : 몇 가지 필드를 쉼표(,)로 구분한 텍스트 데이터 및 텍스트 파일
2. XML(eXtensible Markup Language) : XML(확장 가능한 마크업 언어)은 HTML과 유사하지만, 미리 정의된 태그가 없는 마크업 언어인 것이 특징. 대신 필요에 맞게 특별히 설계된 태그를 직접 정의하는 방식으로 사용됨.
3. JSON(JavaScript Object Notation) : Javascript 객체 문법으로 구조화된 데이터를 표현하기 위한 문자 기반의 표준 포맷입니다. 웹 어플리케이션에서 데이터를 전송할 때 일반적으로 사용(서버-클라이언트 간 데이터를 전송하여 표현)

- 직렬화
  - 데이터 구조나 객체 상태를 저장하고 나중에 재구성할 수 있는 포맷으로 변환하는 과정
  - 객체를 파일의 형태로 저장하거나, 통신하기 쉬운 포맷으로 변환하는 과정
  - 클래스 내부의 필드에 다른 클래스가 있다면 모두 직렬화 처리를 해줘야함
- 역직렬화
  - 파일의 형태(JSON, XML)로부터 객체를 읽어들이는 과정

- Dart의 직렬화
  - 직렬화 : 클래스 -> Json (**toJson() 메서드 이용**)
  - 역직렬화 : Json -> Class (**fromJson() 생성자 이용**)
  ```dart
  class User {
    final String name;
    final String email;
  
    User(this.name, this.email);
  
    // 역직렬화
    User.fromJson(Map<String, dynamic> json)
        : name = json['name'],
          email = json['email'];
  
    // 직렬화
    Map<String, dynamic> toJson() => {
      'name': name,
      'email': email,
    };
  }
  ```


- String 형태 Json을 Map으로 변환 시 ```jsonDecode()``` 함수 사용
  ```dart
  import 'dart:convert';
  
  String jsonString = '{"name": "John Smith", "email": "john@example.com"}';
  Map<String, dynamic> json = jsonDecode(jsonString);
  ```

- Map을 Json 형태의 String으로 변환 시 ```jsonEncode()``` 함수 사용
  ```dart
  import 'dart:convert';
  
  Map<String, dynamic> json = {"name": "John Smith", "email": "john@example.com"};
  String jsonString = jsonEncode(json); 
  ```

--- 
