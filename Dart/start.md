## [Dart 입문]


### Dart 언어의 특징
  1. 컴파일 언어
     - 코드가 실행되기 전 컴파일러를 거쳐서 기계어로 모두 변환되어 실행되는 프로그래밍 언어
     - cf) JavaScript는 인터프리터 언어
  2. Type Safe한 특징을 지님.
     - 컴파일러에 의해 자동으로 데이터 타입이 바뀌지 않음(Type casting은 되지만, Type conversion은 되지 않음.)


### Dart 단일 클래스 자료형
  1. 변수 Data Type 명시(**기본 자료형**): **int(정수), double(실수), String(문자열), bool(논리)**
     ```dart
     int intNum = 1;
     double doubleNum = 1.1;
     String hello = '안녕하세요';
     bool logic = true; //false
     ```
     
  2. 변수 Data Type을 직접 지정하지 않는 경우 : **var, dynamic** -> 기본 자료형을 추론
     - dynamic : Data Type을 추론하여 Type 할당됨. 이후에도 형 변환이 가능함.
       ```dart
       dynamic num = 1;
       dynamic num = 1.1;
       ```
       
     - var : Data Type을 추론하여 Type 할당됨. 단, 이후 형변환이 불가능함.
       ```dart
       dynamic num = 1;
       dynamic num = 1.1; // 불가능
       ```
      
    
  3. 상수 Data Type : **const, final** (**한 번 선언하면, 값이 바뀌지 않는다.**)
     - 공통점 : 모두 상수 할당 시 사용하는 type
     - 차이점 : **final 문법을 통해서 만든 상수는, 초기화하지 않고 만들어지고 나서 상수에 값을 저장할 수 있다.**
       - const 상수 = 1; (컴파일 시 바로 작동, 사용시 반드시 초기화) : 프로그램의 시작 시점에서 상수에 저장할 값을 알 수 있을 때 사용
         ```dart
         const int num = 1.0;
         ```
       - final 상수; (런타임 시 작동, 초기화 하지 않고도 할당 가능) : 프로그램이 시작된 후 계산에서 의해서 상수 값 만들때 사용
         ```dart
         final int num = 1.0;
         ```
         ```dart
         final int num; // const int num; 은 불가
         num = 1.0; 
         ```


### Dart 복수 클래스 자료형(컬렉션)
  1. List : 순서대로 쌓여있는 구조 (중복 허용) [(참고)](https://dart-tutorial.com/collections/list-in-dart/)
  2. Set : 키와 값의 쌍으로 구성 (키의 중복 불가) [(참고)](https://dart-tutorial.com/collections/set-in-dart/) 
  3. Map : 순서가 없는 집합(중복 불가) [(참고)](https://dart-tutorial.com/collections/map-in-dart/) 
     

### Dart 코딩 컨벤션
  - Dart에서는 **" "**(Double Qoutes)보다 **' '**(Single Quotes)를 사용할 것을 권장 (cf. Java 같은 경우 "" 를 사용)
  - 형 변환시 as는 사용하지 않는 것을 권장 (**변환 불가능할 경우 에러가 발생**)


### Type Casting
1. **int, double -> string**
   ```dart
   str = intNum.toString();
   str = doubleNum.toString();
   ```
2. **String -> int, double**
   ```dart
   int intNum = int.parse(str);
   int doubleNum = double.parse(str);
   ```

  
### 입력
  ```dart
  import 'dart:io' // input&output 패키지 불러오기 (stdin, stdout 사용)
  
  void main() {
  String str = stdin.readLineSync()!; // 입력 type이 문자열일 경우
  int intNum = int.parse(stdin.readLineSync()!); // 입력 type이 정수일 경우
  double doubleNum = double.parse(stdin.readLineSync()!); // 입력 type이 실수일 경우
  List<String> input = stdin.readLineSync()!.split(' '); // 한 줄에 공백으로 구분된 값들 불러오기
  }
  ```

### NULL Safety
- Dart는 변수 타입이 기본 자료형(String, int, double, bool) type인 경우, **값이 null(없음)이 될 수 없다.**
  - 컴파일러에서 코드를 실행하기 전에 NULL로 인한 에러를 찾아주어 문법 오류를 미리 지적해준다. (**Null Safety**)
  ```dart
  int str = null; // 불가능
  ```

  - 단, 타입 앞에 ```?```을 명시할 때는 null로 초기화하여도 에러가 나지 않게 할 수 있다. (**Nullable**)
  ```dart
  int str = null; // 불가능
  ?int str = null; 가능
  ```

  
### NULL 처리에 관한 기능
1. **?? (권장)** : 앞에 객체가 null인 경우 ?? 뒤에 작성한 값으로 변환된다.
    ```dart
    int value = nullableValue ?? 0
    ```
2. **! (권장하지 않음)** : nullable인 값을 Null이 아님을 보증할 때 사용. (개발자에게 책임이 따름.)
   ```dart
   int? nullableValue = 10;
   int value = nullableVAlue!;
   ```
3. **?.** : nullable 객체를 안전하게 사용하고자 할 때 사용, null이 아니면 해당 코드를 수행하고 null이면 null을 반환
   ```dart
   int? nullableValue = 10;
   print(nullableValue?.toString()); // 10 출력
   ```

   ```dart
   int? nullableValue = null;
   print(nullableValue?.toString()); // null 출력
   ```
