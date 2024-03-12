## [Dart 기초]


### Dart 언어의 특징
  1. 컴파일 언어(코드가 실행되기 전 컴파일러를 거쳐서 기계어로 모두 변환되어 실행되는 프로그래밍 언어) (cf. 반대 : JavaScript는 인터프리터 언어.)
  2. Type Safe한 특징을 지님. (Type casting은 되지만, Type conversion은 되지 않음. 즉, 컴파일러나 인터프리터에 의해 자동으로 데이터 타입이 바뀌지 않음)


### Dart 단일 클래스 자료형
  1. 변수 Data Type: **int(정수), double(실수), String(문자열), bool(논리)**  *~ 기본 자료형*
  2. 변수 Data Type을 직접 지정하지 않는 경우 : **var, dynamic**
     - var : Data Type을 추론하여 Type 할당됨. 단, 이후 형변환이 불가능함.
     - dynamic : Data Type을 추론하여 Type 할당됨. 이후에도 형 변환이 가능함.
  3. 상수 Data Type : **const, final**
     - 공통점 : 모두 상수 할당 시 사용하는 type. (상수 : 한 번 선언하면, 값이 바뀌지 않는다.)
     - 차이점 : **final 문법을 통해서 만든 상수는, 초기화하지 않고 만들어지고 나서 상수에 값을 저장할 수 있다.**
       - const 상수 = 1; (반드시 초기화; 컴파일 시 바로) : 프로그램의 시작 시점에서 상수에 저장할 값을 알 수 있을 때 사용
       - final 상수; (초기화 없이 먼저 할당한 후, 이후 값 할당 가능) : 프로그램이 시작된 후 계산에서 의해서 상수 값 만들때 사용


### Dart 복수 클래스 자료형
  1. List[(참고)](https://dart-tutorial.com/collections/list-in-dart/)
  2. Set[(참고)](https://dart-tutorial.com/collections/set-in-dart/)
  3. Map[(참고)](https://dart-tutorial.com/collections/map-in-dart/)


### Dart 코딩 컨벤션
  - Dart에서는 **" "**(Double Qoutes)보다 **' '**(Single Quotes)를 사용할 것을 권장 (cf. Java 같은 경우 "" 를 사용)
  - 형 변환시 as는 사용하지 않는 것을 권장 (**변환 불가능할 경우 에러가 발생**)


  
### Type Casting
1. **int, double -> string**
   ```
   str = intNum.toString();
   str = doubleNum.toString();
   ```
2. **String -> int, double**
   ```
   int intNum = int.parse(str);
   int doubleNum = double.parse(str);
   ```

  
### 입력 받아오기 (알고리즘 문제 풀이 시 사용)
  ```
  import 'dart:io'
  String str = stdin.readLineSync()!; // 문자열
  int integer = int.parse(stdin.readLineSync()!); // 정수
  double double = double.parse(stdin.readLineSync()!); // 실수
  List<String> input = stdin.readLineSync()!.split(' '); // 한 줄로 공백으로 구분된 여러 값 불러오기
  ```
