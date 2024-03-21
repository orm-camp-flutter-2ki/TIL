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
      - try{ }에서 에러가 났을 때, 예측한 on ```ErrorType``` 인 경우 ErrorType { }을 실행
      - try{ }에서 에러가 났을 때, on ErrorType이 아닌 다른 경우 catch { }을 실행
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
2. XML(eXtensible Markup Language) : XML(확장 가능한 마크업 언어)은 HTML과 유사하지만, 미리 정의된 태그가 없는 마크업 언어. 대신 필요에 맞게 특별히 설계된 태그를 직접 정의하는 방식으로 사용됨.
3. JSON(JavaScript Object Notation) : Javascript 객체 문법으로 구조화된 데이터를 표현하기 위한 문자 기반의 표준 포맷. 웹 어플리케이션에서 데이터를 전송할 때 일반적으로 사용(서버-클라이언트 간 데이터를 전송하여 표현)

- 직렬화
  - 객체를 파일의 형태로 저장하거나, 네트워크를 통해 전송할 수 있는 형태로 변환하는 과정
  -  **클래스 내부의 필드에 다른 클래스가 있다면 모두 직렬화 처리를 해줘야한다.**
- 역직렬화
  - 직렬화된 파일이나 데이터를 읽어들여 다시 데이터 구조나 객체를 복원하는 과정
  - 직렬화된 데이터를 읽어들여서 원래의 객체나 데이터 구조를 재구성
    
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

### <디버깅>
- 개념 : 소프트웨어의 오류를 식별하고 수정하는 과정
- 중요성 : 소프트웨어가 올바르게 작동하는지 확인하는데 필수적 (하지 않으면 오류 발생하거나, 제대로 작동하지 않음)
- 디버깅 기술
  - 로깅(Logging) : 코드가 실행되는 동안 발생하는 이벤트를 기록
    - Flutter에서는 ```debugPrint()``` 등을 활
  - 중단점(Breakpoint) : 코드의 특정 지점에서 실행을 중지하는데 사용
    ![image](https://github.com/algochemy/TIL/assets/152131529/c8ef73cd-58c8-4e00-96da-a9b5352bfded)
  - 디버거(Debugger) : 디버깅을 도와주는 도구. 디버거 모드로 실행하여 브레이크 포인트에서 멈추거나 에러가 나면 다양한 도구를 활용하여 에러를 찾는데 도움이 된다
    ![image](https://github.com/algochemy/TIL/assets/152131529/a9d729c5-316d-4364-a505-32b057e868fb)
  - 스택 추적 : 호출 스택을 추적하여 코드가 실행 중인 위치를 확인하는데 사용
  ![image](https://github.com/algochemy/TIL/assets/152131529/81e8d9c5-7e9c-47e6-b9d4-c8431ad5c8a0)

- 디버깅 팁 (중요)
  - 작게 시작 :  한 번에 한 가지 문제에 집중하기 (큰 문제로 넘어가기 전에 작은 문제부터 시작)
  - 단순하게 유지 : 디버깅 시 코드를 단순하게 유지하기 (오류의 원인을 파악하기 더 쉬움)
  - 인내심 유지 : 디버깅은 시간이 많이 걸릴 수 있음 (오류를 즉시 찾지 못해도 포기하지 말것)

---

### <람다식과 함수>
- 개념
  - [1급 객체(first-class object)](https://dart.dev/language/functions#functions-as-first-class-objects) : 함수를 다른 함수의 매개변수로 전달할 수 있다.
    ```dart
    void main() {

    void printElement(int element) {
    print(element);
    }

    var list = [1, 2, 3];

    // Pass printElement as a parameter.
    list.forEach(printElement);
    }
    ```
    - 대표적인 1급 객체 : 값, 인스턴스, 함수

 - 함수를 람다식으로 표현하기 : 함수에 **단일 표현식**이나 **return 문만 포함**되어 있는 경우 ```=>``` 표기법을 사용하여 이를 단축할 수 있다. 
   - 기본 함수형태 (람다식 적용 X)
   ```dart
   bool isNoble(int atomicNumber) {
     return _nobleGases[atomicNumber] != null;
   }
   ```
   - 람다식 적용한 형태 (```{}``` 와 ```return``` 을 지우고, ```=>``` 을 사용)
     ```dart
     bool isNoble(int atomicNumber) => _nobleGases[atomicNumber] != null;
     ```

  - [익명 함수](https://dart.dev/language/functions#anonymous-functions) : 이름이 없는 함수
    ```dart
    // 기존 함수(이름이 있음 : printElement)
    void printElement(int element) {
      print(element);
    }

    // 익명 함수(이름이 없음)
    var list = [1,2,3]
    list.forEach(element) { print(element); });
    ```

  - 함수형 프로그래밍
    - 다트는 객체지향 프로그래밍(OOP)과 함수형 프로그래밍(FP) 특징을 모두 제공하는 멀티 패러다임 언어
    - 함수형 프로그래밍은 자료 처리를 수학적 함수의 계산으로 취급하는 프로그래밍 패러다임
    - 가변 데이터를 멀리하는 특징을 가짐

  - 고계 함수(high-order function) : 함수를 파라미터로 받는 함수
    - [where](https://dart.dev/codelabs/iterables#mapping) : 조건 필터링
      - where의 output은 Iterable 이다. 필터링 결과를 리스트나 셋 형태로 출력하려면 ```toList()```, ```toSet()``` 사용
        ```dart
        List<int> numbers = [1,2,3,4,5];
        Iterable<int> evenNumbers = numbers.where((number) => number.isEven);
        print(evenNumbers); // (2, 4)
        ```
        
    - [map](https://dart.dev/codelabs/iterables#mapping) : 모든 요소에 함수를 적용(각 요소에 함수를 적용하여 각 요소를 새 요소로 변환)
      ```dart
      List<int> numbers = [1,2,3,4,5];
      Iterable<int> output = numbers.map((number) => number * 10); // (10, 20, 30, 40, 50)
      ```
      ```dart
      List<int> numbers = [1,2,3,4,5];
      Iterable<String> output = numbers.map((number) => number.toString()); // (1, 2, 3, 4, 5)
      ```
      - map은 요소가 반복될 때만 제공된 함수가 호출된다.
     
    - [forEach](https://api.dart.dev/stable/3.3.2/dart-core/Iterable/forEach.html) : for in 반복문에서, 전체 요소를 반복하는 경우 사용
      ```dart
      List<int> collection = [1, 2, 3];
      collection.forEach(print);
      // 1
      // 2
      // 3
      ```
    
    - [reduce](https://api.flutter.dev/flutter/dart-core/Iterable/reduce.html) : **컬렉션의 요소를 반복적으로 결합하여 컬렉션을 단일 값으로 줄임(reduce)**
      ```dart
      final numbers = <double>[10, 2, 5, 0.5];
      final result = numbers.reduce((value, element) => value + element);
      print(result); // 17.5
      ```
    
    - [fold](https://api.flutter.dev/flutter/dart-core/Iterable/fold.html) : **컬렉션의 각 요소를 기존 값과 반복적으로 결합하여 컬렉션을 단일 값으로 줄임**
      ```dart
      final numbers = <double>[10, 2, 5, 0.5];
      const initialValue = 100.0;
      final result = numbers.fold<double>(initialValue, (previousValue, element) => previousValue + element);
      print(result) // 117.5;
      ```

    - [any](https://api.flutter.dev/flutter/dart-core/Iterable/any.html) : 하나 이상의 요소가 조건을 만족하면 true를 반환
      ```dart
      final numbers = <int>[1, 2, 3, 5, 6, 7];
      var result = numbers.any((element) => element >= 5); // true;
      result = numbers.any((element) => element >= 10); // false;
      ```

    - [every]() : 모든 요소가 조건을 만족하면 true를 반환
      ```dart
      final planetsByMass = <double, String>{0.06: 'Mercury', 0.81: 'Venus', 0.11: 'Mars'};
      // Checks whether all keys are smaller than 1.
      final every = planetsByMass.keys.every((key) => key < 1.0); // true
      ```


  - [Iterable](https://dart.dev/codelabs/iterables) : 반복 가능한 컬렉션, 순차적으로 액세스 할 수 있는 요소의 컬렉션
    - List: 인덱스를 기준으로 요소를 읽는 데 사용
    - Set: 한 번만 발생할 수 있는 요소를 포함하는 데 사용
    - Map: 키를 사용하여 요소를 읽는 데 사용
   
  - [Iterator](https://api.flutter.dev/flutter/dart-core/Iterable/iterator.html) : Iterable(반복 가능한 객체)의 요소를 반복하게 하는 것
    ```
    Iterator<E> get iterator;
    ```
    - Iterator가 읽힐 때 마다, 새로운 Iterator를 반환하고 전체 요소에 반복될 때 까지 반복할 때 사용된다.
    - 기존 컬렉션이 변경되지 않는 한, 동일한 요소를 동일한 순서로 반환해야 한다.
    - 컬렉션 수정 시 새 반복자가 다른 요소를 생성할 수 있고, 기존 요소의 순서가 바뀔 수 있다.

---
