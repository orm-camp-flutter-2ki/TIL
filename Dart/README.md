## [Flutter 작업환경 설정]

### 1. Flutter 설치
  1. [Flutter 공식 홈페이지](https://flutter-ko.dev/get-started/install) 을 통해 다운로드 및 압축해제 (flutter 폴더가 생성된다.)
  2. [Visual Studio 2022 다운로드](https://visualstudio.microsoft.com/ko/vs/community/) (Visual Studio Code 아님.)
  3. [Andorid Studio 다운로드](https://developer.android.com/studio/install) : [Plugins] 에서 Dart, Flutter 검색하여 설치  

### 2. 환경변수 설정
  - **'C:\Program Files\Flutter' 경로에 플러터 폴더가 위치해있다고 하면, 하위 폴더 bin 까지의 경로를 복사하여
    *C:\Program Files\Flutter\bin* 을 시스템 변수 Path에 추가한다.** (공식 홈페이지에서는 'C\Program Files'에 다운받는 것을 권장하지 않으니 참고할 것. 본인은 다른 경로에 압축파일을 푼 다음에 위치를 변경하였다.)
    - CMD을 이용한 환경변수 설정은 다음과 같이 할 수 있다.
    ```
    setx path %path%; C:\Program Files\Flutter\bin;
    ```


### 3. Flutter 설치현황 확인
  - 설치가 잘 되어있는지 *간단히*  확인할 수 있는 명령어
    ```
    flutter doctor
    ```
  - 설치가 잘 되어있는지 *자세히*  확인할 수 있는 명령어 (설치된 경로 조회 시 유용)
    ```
    flutter doctor -v
    ```

### 4. Dart 버전 확인
  ```
  dart --version
  ```

### 5. Flutter 최신버전 업데이트 ( *필요시 사용* )
  ```
  flutter upgrade
  ```
  
### 6. Dart 프로젝트 폴더 생성 [(참조링크)](https://dart.dev/tutorials/server/get-started#3-create-a-small-app)
  ```
  dart create -t console 프로젝트폴더명
  ```
---

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

  
  
### NULL Safety
  ```
  int str = null; // 불가능
  ?int str = null; 가능
  ```
  - Dart는 윗줄과 같은 경우 컴파일러에서 코드를 실행하기 전에 NULL로 인한 에러를 찾아주어 문법 오류를 미리 지적해준다. (Null Safety)
  - 단, 아래줄과 같이 타입 앞에 ?을 명시할 때는 입력으로 NULL을 받아도 에러가 나지 않게 할 수 있다. (Nullable)

  

  
### NULL 처리에 관한 기능
1. **?? (권장)** : 앞에 객체가 null인 경우 ?? 뒤에 작성한 값으로 변환된다.
    ```
    int value = nullableValue ?? 0
    ```
2. **! (권장하지 않음)** : nullable인 값을 Null이 아님을 보증할 때 사용. (개발자에게 책임이 따름.)
   ```
   int? nullableValue = 10;
   int value = nullableVAlue!;
   ```
3. **?.** : nullable 객체를 안전하게 사용하고자 할 때 사용, null이 아니면 해당 코드를 수행하고 null이면 null을 반환
   ```
   int? nullableValue = 10;
   print(nullableValue?.toString()); // 10 출력

   
   int? nullableValue = null;
   print(nullableValue?.toString()); // null 출력
   ```

## [객체 지향 프로그래밍, OOP]
- 오브젝트(객체) : 현실 세계의 모든 객체 : **상태(속성)과 동작으로 구성**
- 클래스 : 객체를 가상세계 용으로 구체화한 것 : **필드와 메소드**
  - **클래스를 정의하면, 그 클래스 타입의 변수를 선언할 수 있다.** (String type도 클래스(레퍼런스 타입)이다.)
- 인스턴스 : 클래스가 컴퓨터 Heap 메모리에 할당된 상태 (*생성자를 통해 할당됨).

- 클래스명 Object가 선언되어있을 때, 인스턴스는 다음과 같이 생성한다.
  ```
  Object object = new Object() // Dart에서는 new가 불필요하다.
  Object object = Object() // new를 생략하고 인스턴스를 생성한다.
  ```
- 생성된 인스턴스의 필드 접근은 **.** 을 이용한다.
  ```
  object.name = 'Name';
  object.num = 1;
  ```

- static 문법 : Class 정의할 때 정적 필드를 정의할 때 사용(인스턴스가 생성되어 있지 않아도, 정적 필드에 접근된다.)
  ```
  class Object {
  static int sNum = 0;
  String name;
  int num;
  Field? field;

  static void func() { ... }
  ```
  
  클래스 Object가 위와 같이 생성돼있다고 하면, static 필드는 인스턴스를 생성하지 않고 다음과 같이 접근 가능
  ```
  void main() {
  Object.func();
  print(Object.sNum);
  }
  ```

  즉, 인스턴스화 하는 과정 불필요
  ```
  // Object object = Object()
  ```
#### 생성자 사용 시 주요 문법
- **데이터 타입이 Null을 허용하지 않으면 required를 붙여야 한다.**
  ```
  class Object {
  String name; // Null 허용 X -> required
  int num; // Null 허용 X -> required
  Field? field;
  
  Object(required this.name, required this.num, this.field);
  }
  ```
  
- **생성자에 { }를 사용하면 선택(Optional 혹은 Named) Parameter이다.**
  - **필수 parameter와 선택 parameter를 동시에 사용할 경우, 필수 parameter가 앞에 와야한다.**
    ```
    class Object {
    String name;
    int num;
    Field? field; // Named Parameter
    
    Object(this.name, this.num, {this.field});
    ```
