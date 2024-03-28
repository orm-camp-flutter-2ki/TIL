# [Dart 중급]

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

 - **함수를 람다식으로 표현하기** : 함수에 **단일 표현식**이나 **return 문만 포함**되어 있는 경우 ```=>``` 표기법을 사용하여 이를 단축할 수 있다. 
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
      print(result);
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

### <비동기 프로그래밍>
<img src="https://github.com/algochemy/TIL/assets/152131529/318d9a4f-e311-4aad-8db1-2695d3b1fa71" height="400px" width="600px">  
  
- 동기(Synchronous)
  - 개념 : 모든 작업은 이전 작업의 실행이 완료될 때까지 기다려야 한다. (하나의 작업이 종료될 때 까지 기다린 후 다음 작업)
  - 특징 : 코드가 순서대로 실행된다.
  - 동기 함수는 동기 작업만을 수행
    
- [비동기(Asynchronous)](https://dart.dev/codelabs/async-await)
  - 개념 : 임의의 순서로 또는 동시에 작업이 실행된다. (두 개 이상의 작업이 동시에 수행)
  - 비동기 처리 방법 : 콜백 함수, Future(비동기 작업 결과 제공), *Stream(비동기 작업 결과가 다수인 경우)*, async - await 방식(비동기 결과와 상호작용)
  - 비동기 함수는 적어도 한 개 이상의 비동기 작업을 수행하며 동기작업도 수행이 가능
  - **장점 : 다른 작업이 완료되기를 기다리는 동안 작업을 완료할 수 있다.**
  - **자주 사용되는 비동기 작업**
    - 네트워크를 통해 데이터를 가져올 때
    - 데이터베이스에 쓰기를 수행할 때
    - 파일로부터 데이터를 읽을 때
  
- Future 클래스
  - 개념 : 미래에 완료되는 객체, 미래에 받아올 값을 의미
    ```dart
    Futrue<String> name;
    Futrue<int> number;
    Futrue<Person> person;
    ```
    ```dart
    Future<T> 
    ```
    Future는 제네릭으로 이해될 수 있다.
  - 지연 문법 : ```Future.delayed(Duration(seconds: A), B)``` : A초 후에 B 작업이 이루어지도록 한다.

  
- [future](https://dart.dev/codelabs/async-await#what-is-a-future)
  - 개념 : Future 클래스의 인스턴스
  - 특징 : 비동기 작업의 결과를 나타내며, 완료(completed)/미완료(uncompleted) 중 한 가지 상태를 가진다. 미완료는 future가 값을 생성하기 전의 상태를 의미한다.
    - 미완료 : 비동기 함수를 호출하면, 미완료된 future를 반환한다. 해당 future는 함수의 비동기 작업이 끝나거나 에러 발생을 기다린다
    - 완료 : 비동기 작업이 성공적으로 끝나면, future는 값으로 완료되고 그렇지 않으면 에러로 완료된다.
      - 값으로 완료 : Future<T> 타입의 future는 T값으로 완료된다. **제너릭**
        - Future<String> 타입의 future는 문자열 값을 생성한다.
        - Future<int> 타입의 future는 정수 값을 생성한다. 
        - Future<void> 타입의 future는 사용가능 한 값을 생성하지 않는 경우 사용 (예: **main 함수 호출 시 사용**)
      - 에러로 완료 : 어떤 이유로 함수가 수행하는 비동기 작업이 실패하면, future는 에러로 완료된다.
 
- [async, await](https://dart.dev/codelabs/async-await#execution-flow-with-async-and-await)
  - async
    - 함수 본문 앞에 키워드를 사용하여 비동기 함수임을 명시, 결과가 event queue로 보내진다.
    - Future 클래스는 {} 앞에 ```async``` 키워드를 지정해줘야 한다.
  - await
    - 비동기 표현식의 완성된 결과를 얻을 수 있다.
    - 대기하고 싶은 비동기 함수를 실행할 때 **```await```키워드를 사용해주면 코드를 작성한 순서대로 실행된다.** (Dart가 await 키워드를 보는 순간, await 뒷 부분은 모두 event 큐로 보내지어, 나머지 함수는 future가 완료될 때 까지 먼저 실행되지 않는다. ---> 즉, 동기 함수라도 먼저 실행되지 않음.)
    - await 키워드는 async 키워드가 있는 함수에서만 사용할 수 있다.
    - **await 키워드 뒤에는 반드시 Future 타입이 와야 한다.**
   
    - 예시
      - async-await 문법을 쓰지 않으면, 동기 함수가 먼저 출력된다. (콜백 사용하는 경우)
        ```dart
        void main() {
          print(1);
        
          Future<int>.delayed(Duration(seconds: 2), () => 2)
              .then((value) {     
            print(value);
          });
         
          print(3);  
        }
        ```
        ```
        1
        3
        2
        ```
   
      - async-await 문법을 쓰면, await 이후 부분의 동기 함수가 나중에 출력된다.
        ```dart
        Future<void> main() async {
          print(1);
    
          int value = await Future<int>.delayed(
             Duration(seconds: 2), 
             () => 2 
          );
          print(value);
        
          print(3);
        }
        ```
        ```dart
        1
        2 // 1 출력되고 -> (2초 대기 후) -> 2가 출력
        3
        ```

- [callback](https://dart.dev/codelabs/async-await#what-is-a-future) : future가 완료되면 콜백을 실행하여 결과를 처리할 수 있다. 이 Future<T>클래스는 콜백을 예약하기 위한 세 가지 메서드를 제공
  - ```then()``` : 값과 함께 성공적으로 완료되면 메서드에 콜백을 추가하여 결과를 얻음 (예외처리의 try 개념과 유사)
  - ```catchError()``` : 오류로 인해 future가 실패하는 경우 오류를 처리 (예외처리의 catch 개념과 유사)
  - ```whenComplete()``` : future의 성공 여부에 관계없이 항상 실행 (예외처리의 finally 개념과 유사)

  - 콜백 처리 예시 (future가 값으로 완료 => callback의 'then' 메소드를 추가하여 value 값을 얻음)
    ```dart
      void main() {
          print(1);
          var future = Future<int>.delayed(Duration(seconds: 1), () => 2);
          future.then((value) => print(value)); // future가 완료되어 then 메서드를 통해 콜백을 추가하여 결과를 얻음
          print(3);
      }
    ```
  
    ```dart
    future
        .then((value) => print('비동기 작업 성공: $value'))
        .catchError((error) => print('비동기 작업 에러: $error'))
        .whenComplete(() => print('종료'));
    ```
    future의 리턴 값이 value라면 입력 파라미터를 value로 해서 value을 출력한다.
    만약 future의 리턴 값이 value가 아니면 원하는 결과가 아니니 catchError()의 내용대로 error을 출력한다.
    future 값이 완료/미완료든 종료를 출력한다.

- **callback vs async-await 어떤걸 쓰는게 좋을까?**
  - callback
    - 특징: 이해하기 쉽지만, 코드를 읽기 어렵다.(특히 값 반환)
      ```dart
      var future = Future<int>.delayed(Duration(seconds: 1), () => 2);
      future.then((value) => print(value));
      ```
  - async-await
    - 특징 : 콜백에 비해, 더 동기 코드처럼 보여진다. 또한, 코드를 읽기 쉽다.(특히 값 반환)
      ```dart
      final value = await Future<int>.delayed(Duration(seconds: 1), () => 2,
      ```
      - async-await 문법을 사용할 시, 콜백의 ```then-catchError-whenComplete``` 대신 ```try-catch-finally``` 문법을 함께 사용한다.
      ```dart
      Future<void> usingAsyncAwaitWithErrorHandling() async {
        print('Before the future');
      
        try {
          final value = await Future<int>.delayed(
            Duration(seconds: 1),
            () => 42,
          );
          print('Value: $value');
        } catch (error) {
          print(error);
        } finally {
          print('Future is complete');
        }
      
        print('After the future');
      }
      ```
---

### <데이터 소스>
- 데이터 소스란?
  - 데이터의 근간이 되는 원천 재료
  - 프로그램이 사용하는 원천 데이터 모든 것이 해당
    - Text, File, JSON, XL, CSV, RDBMS, NoSQL, etc...
  - **DataSource에서 추출한 가공되지 않은 데이터를 사용가능한 데이터로 변환**해야 한다.
    - [Json과 데이터 클래스의 상호변환](https://docs.flutter.dev/data-and-backend/serialization/json)
      - 서버와 통신을 대부분 JSON으로 함
      - 서버로부터 JSON 데이터 받기 (역직렬화)
        - 서버에서 보내는 것은 문자열 형태의 Json이므로, 먼저 Dart의 Map 형태로 바꾼다. ```Map<String, Dynamic> json = jsonDecode(jsonString);```
        - 이후 Map 자료구조인 json을 fromJson 생성자를 통해 ModelClass(데이터 클래스로)로 변환한다.
          ```dart
          class User {
            final String name;
            final String email;
          
            User(this.name, this.email);
          
            User.fromJson(Map<String, dynamic> json)
                : name = json['name'] as String,
                  email = json['email'] as String;
          ```
        
       
  - [http 통신](https://pub.dev/packages/http)
    - 프로젝트 폴더에서 터미널을 열고 다음을 설치 (윈도우 환경에서 Android Studio 사용할 경우 ```Alt+F12```로 터미널 접근)
      ```cmd
      dart pub add http
      ```

    - 통신 예
      ```dart
      import 'package:http/http.dart' as http;
  
      var url = Uri.https('example.com', 'whatsit/create');
      var response = await http.post(url, body: {'name': 'doodle', 'color': 'blue'});
      print('Response status: ${response.statusCode}');
      print('Response body: ${response.body}');
      
      print(await http.read(Uri.https('example.com', 'foobar.txt')));
      ```
      
---

### <Model Class, Repository 개념>

- 모델 클래스
    - 정의 : **별도의 기능을 가지지 않는 순수한 클래스로서, 모델 객체 클래스의 속성에 대한 데이터를 조회할 수 있는 클래스**를 의미한다.  **View에 보여질 데이터를 담는 객체**로 이해될수 있다.
      - 데이터 클래스 6종 필요하면 추가하여 사용! (**이는 별도의 기능으로 보지 않는다.**)
        - 재정의 ==, hashCode (동등성 비교)
        - 재정의 toString (출력)
        - 생성자 fromJson (역직렬화)
        - 메소드 toJson (직렬화)
        - 메소드 copyWith (깊은 복사)
    
    - 역할 : 데이터 소스를 앱에 필요한 형태로 변환하여 앱 개발을 편리하게 해주는 역할
    - 예시
      ```
      class User {
        final String name;
        final int age;
      
        User(this.name, this.age);
      // 데이터 클래스 추가
      }
      ```
      
- 모델링 방법
  - DDD(Domain Driven Design) : 도메인 기반(주도) 설계
    - Domain 이란?
      - 유사한 업무의 집합
      - 특정 상황(주문,결제,로그인)이나 특정 객체(유저, 손님)가 중심이 될 수 있음
    - Model Class 결론
      - 모델 클래스를 정의하는 방법은 여러가지가 있음
      - 프로젝트의 성격에 따라 다양한 방식으로 모델 클래스를 정의할 수 있음
      - 데이터 클래스 6종 세트가 필요하면 추가하여 사용
      - 예시
        ```dart
        class User {
          final String name;
          final int age;
  
          factory User.fromJson(Map<String, dynamic> json) {
            return User(json['name'], json['age']);
          }
  
          @override
          String toString() => 'User(name: $name, age: $age)';
        }
        ```
        
  - ORM(Object-relational mapping) : 데이터 소스가 DB인 경우 DB와 모델간 상호 변환을 도와주는 기법


- 디자인 패턴: SW 개발에서 설계 문제에 대한 해답을 문서화하기 위해 고안된 형식 방법

- Factory 생성자
  - 특징 : 클래스 유형의 개체를 반환하는 특수한 생성자이다. 일반 생성자는 클래스 자체의 새 인스턴스만 만들 수 있는 반면, Factory 생성자는 기존 인스턴스 또는 하위 클래스를 반환할 수 있다. 특히, 사용하는 코드에서 클래스의 구현 세부 정보를 숨기고 싶을 때 유용하다.

  - 일반적인 생성자를 사용한 예 (factory 생성자 사용 X)
    ```dart
    User.fromJson(Map<String, Object> json)
      : _id = json['id'] as int,
        _name = json['name'] as String;

    final map = {'id': 10, 'name': 'Sandra'};
    final sandra = User.fromJson(map);
    ```
    위 방식을 이용하면, 만약 'id'나 'name'이 map에 존재하지 않으면 null을 처리하지 않기 때문에 앱이 다운되는 문제가 있다.

  - factory 생성자를 사용한 예
    ```dart
    factory User.fromJson(Map<String, Object> json) {
      final userId = json['id'] as int;
      final userName = json['name'] as String;
      return User(id: userId, name: userName);
    }

    final map = {'id': 10, 'name': 'Sandra'};
    final sandra = User.fromJson(map);
    ```
    factory 생성자는 위 fromJson() 예시에서, 새 개체를 반환하기 전에 작업을 수행할 수 있도록 허용하고, 그 작업의 세부 사항을 클래스를 사용하는 사람에게 노출하지 않게 한다. 또한, factory 생성자를 사용하면 객체를 만들기 전에 모든 종류의 검증, 오류 검사, 인수 수정까지 할 수 있으므로 -> null을 처리하지 못해서 앱이 다운되는 경우를 방지할 수 있다.

 
 - Singleton 패턴
   - 정의 : 1개의 인스턴스만 생성되는 것을 보증하기 위한 패턴
   - 특징 : 인스턴스 생성을 여러번 시도해도 1개의 인스턴스가 공유됨
   - 구현방법 : **팩토리 생성자를 사용하여 싱글톤 패턴을 구현할 수 있다.** (팩토리 생성자는 객체의 새 인턴스를 반환할 필요가 없기 때문)
   - 용례 : 캐시나 공유 데이터, 처리의 효율화에 사용되는 테크닉, 데이터베이스에 대한 여러 연결을 방지
   - 예시
     ```dart
     // 싱글턴 패턴
     class RentCar {
       static final RentCar _instance = RentCar._internal();

       int _count = 0;

       RentCar._internal();

       factory RentCar.getInstance() {
         return _instance;
       }

        void increment() {
          _count++;
        }
      }
      
     void main() {
       final car1 = RentCar.getInstance();
       final car2 = RentCar.getInstance();

       car1.increment();
       print(identical(car1, car2));
       print(car2._count);
     }
     ```
    -> 싱글턴 패턴으로 인해 car1, car2 인스턴스는 2개의 인스턴스가 생성된게 아니라 동일한 1개의 인스턴스이다.
  
  - Repository 패턴
    - 정의 : SW 개발에서 **데이터 저장소에 접근하는 객체를 추상화**하고, 데이터소스(DB, File)와의 **통신을 담당하는 객체를 캡슐화**하는 디자인 패턴
    - 구성요소
      - Client : 데이터 요청을 시작하는 구성요소 (cf. 서비스, 컨트롤러)
      - Repository
        - 책임과 역할 : 데이터 소스와 상호작용하여 데이터를 추가,조회,수정,삭제하는 역할을 담당
        - 패턴 : **데이터 액세스 추상화** 비지니스 로직과 데이터를 분리함으로써 여러가지 이점을 얻음
      - DataSource : REST API, DB, File 등..
    - [구현](https://github.com/algochemy/learn_dart_together/tree/master/lib/240326/repository)
      - 1. 모델 클래스 생성 ```class Todo```
      - 2. Repository 인터페이스 생성 ```abstract interface class TodoRepository```
      - 3. Repository 클래스 구현 ```class TodoRepositoryImpl implements TodoRepository```

---

### <단위 테스트>
- 정의 : 특정 모듈이 의도한 대로 잘 작동하는가를 테스트하는 가장 작은 단위의 테스트 (*모듈 = 메서드, 기능)
- 단위 테스트가 꼭 필요한 경우
  - DB
    - 스키마가 변경되는 경우
    - 모델 클래스가 변경되는 경우
  - Network
    - 예측한 데이터가 제대로 들어오는지
  - 데이터 검증
    - 예측한 데이터를 제대로 처리하고 있는지

- 테스트 방법 종류
  - 수동 테스트 : 인간이 하는 테스트 (print)
  - 단위 테스트 : 1개의 함수를 테스트 (test 코드)
  - 통합 테스트 : 여러개 연관된 클래스나 함수를 함께 테스트 (UI test, Integration test)
 
- 화이트 박스 테스트
  - 내부 구조와 동작에 중점을 두고 테스트하는 방법
  - 코드의 내부 로직, 제어 흐름, 데이터 흐름 등을 이해하고 검증하는 데에 사용
  - 테스트 케이스를 설계할 때 코드의 특정 부분을 직접 확인
  - 주요 기법으로는 구문 검사, 경로 검사, 조건/분기 검사 등이 있다

- 블랙박스 테스트
  - 소프트웨어의 내부 구조를 무시하고 기능을 테스트하는 방법
  - 시스템이 어떻게 동작하는지에 대한 내부 정보를 알 필요 없이 사용자 관점에서 테스트
  - 테스트 케이스는 입력 값과 예상 출력 값에 기반하여 설계
  - 요구 사항을 충족하는지 확인하고, 시스템의 기능적 및 비기능적 요구 사항을 테스트
  - 주요 기법으로는 등가 분할, 경계 값 분석, 상태 전이 테스트 등이 있다

- 테스트의 장점
  - 장애에 관한 신속한 피드백
  - 개발 주기에서 조기 장애 감지
  - 회귀에 신경 쓸 필요 없이 코드를 최적화할 수 있도록 하는 더 안전한 코드 리팩터링
  - 기술적 문제를 최소화하는 안정적인 개발 속도

- 테스트 케이스
  - 가능한 모든 가능성의 범위를 테스트하는 것이 좋은 테스트 케이스이다
  - 동등 분할, 경계값 분석... 등의 기법 등이 있음
 
- 테스트 환경 및 실행
  - 테스트 코드는 원래 파일에 _test 를 붙이고 동일 위치에 생성한다
    ![image](https://github.com/algochemy/TIL/assets/152131529/9df28398-529b-4d29-9dde-7f01694e96f4)

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
       - ```expect(a, throwException)``` 와 같이 예외 처리를 할 수도 있다. (반대는 returnNormally)
     - test 함수가 여러개일 시, group() 으로 test('테스트', (){}); 을 묶어서 테스트 할 수 있다.
    - 테스트 코드 실행은 Debug 모드로 실행한다.
    - 테스트가 성공하도록 코드를 수정, 테스트 중심으로 개발하는 방법론을 TDD (Test Driven Development)라고 한다.

- [Test Double](https://en.wikipedia.org/wiki/Test_double)
  - 테스트를 진행하기 어려운 경우에 테스트가 가능하도록 만들어주는 객체 (어원 : 영화 촬영 시 위험한 역할을 대신하는 스턴트 더블에서 비롯)
    - <img src="https://github.com/algochemy/TIL/assets/152131529/49cedd7d-0cb0-4d94-812d-d13de5d91ff6" height="400px" width="600px">  
  - [Test Double의 경계](https://learn.microsoft.com/en-us/archive/msdn-magazine/2007/september/unit-testing-exploring-the-continuum-of-test-doubles)는 모호하므로, 엄밀하게 용어 구분하는 것은 불필요하다.
    - <img src="https://github.com/algochemy/TIL/assets/152131529/43dfdada-2c49-45c1-ae13-dc0c6a676e8a" height="400px" width="600px">


- 테스트 용이성
  - 다형성을 활용하면 테스트할 때 원하는 객체를 활용 가능
  - 테스트용 객체를 별도로 준비하여 테스트 가능

---

### <Dto>  

- DTO(Data Transfer Object) 
  - Dto : 데이터 소스를 모델 클래스로 변환하는 과정에서 순수하게 클래스에 담기 위한 중간 전달 객체 (**JSON -> DTO -> Model Class**)
  - Mapper : **순수한 데이터 소스 (Dto) 를 원하는 모델 클래스로 변환하려면 fromJson(), toJson() 처럼 변환 기능이 필요**한데, 이를 Mapper 라고함.**(Mapper : DTO -> Model**)

- DTO 가 필요한 이유
  - Model Class는 non-nullable 한 값만 가지고 있도록 한다
  - Json 데이터는 Null 값을 포함시킬 수 있음
  - Map -> Model Class 변환 시 null 값 등의 예외를 사전에 걸러내기 용이함 (불완전한 코드가 포함될 것 같다면 Dto를 도입하자)
  - Json 값에 예외가 없다면 반드시 Dto를 도입할 필요는 없다

- 구현 방법
  - 모델 클래스
    - 모델 클래스는 불변 객체만을 담도록 한다. (모든 필드가 ```final```인 non-nullable 상수를 가지게 하고, ```const```인 생성자를 가지게 한다.) 그리고 옵션으로 ```toString, ==, hashCode, copyWith``` 4가지 메소드에 대해서만 재정의를 한다.( ```fromJson, toJson``` 은 Dto 클래스에서 작성한다.)

  - Dto
    - **Dto 클래스 작성을 위해서는 JsonToDart 플러그인을 설치해 사용**한다. ```fromJson(), toJson()```을 만을 담는다.

  - Mapper
    - Dto를 Model 클래스로 변환하는 유틸 메소드이다. [확장함수 활용](https://dart.dev/language/extension-methods) ```extensiton TempDtoToTemp on TempDto```
    - Nullable을 non-Nullable로 변환하는것이 핵심
    - Dto 전체를 변환하는 것이 아니라, 필요한 부분만 변환한다.
   
---
