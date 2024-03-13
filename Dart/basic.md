# [Dart 기초]

## 객체 지향 프로그래밍, OOP
- 오브젝트(객체) : 현실 세계의 모든 객체 : **상태(속성)과 동작으로 구성**
- 클래스 : 객체를 가상세계 용으로 구체화한 것 : **필드와 메소드**
  - 클래스를 정의하면, 그 클래스 타입의 변수를 선언할 수 있다.(String type도 클래스(레퍼런스 타입)이다.)
- 인스턴스 : 클래스가 컴퓨터 내의 Heap 메모리에 할당된 상태 : **인스턴스는 ```생성자```를 통해 생성됨**

1. 클래스 및 생성자 정의
   - a. 클래스명은 대문자로 시작하고, 클래스가 가지는 필드명을 정의한다.
     ```dart
     // 클래스
     class Object {
     // 필드(멤버변수)
     String name;
     int num;
     }
     ```

   - b. 생성자/메소드를 함께 정의한다.
     ```dart
     // 클래스
     class Object {
     // 필드
     String name;
     int num;
     // 생성자
     Object(this.name, this.num);
     // 메소드
     void study() {
     print('공부합니다.');
     }
     }
     ```
     - 생성자 : Object(this.name, this.num) ```여기서 this는 현재 클래스 Object을 의미
     - 메소드 : 클래스 내에서 동작하는 함수 ```[반환타입] [함수명]() {}```
     
  
2. 인스턴스 생성
   - 클래스명 Object가 선언되어있을 때, 인스턴스는 다음과 같이 생성한다. ```클래스명 인스턴스명 = 클래스명(생성자)```
     ```dart
     // Object object = new Object() // Dart에서는 우항의 생성자 생성을 위한 new 문법이 불필요하다.
     Object object = Object() // 즉, new를 생략하고 인스턴스를 생성한다. 
     ```     
   - 인스턴스가 가진 필드/메소드 값은 ```인스턴스명.필드명``` 으로 접근할 수 있다.
     ```dart
     print(object.name);
     print(object.num);
     object.study();
     ```
     
   - 1-b에 대한 프로그램 실행(결과)
     ```dart
     void main() {
     Object object = Object('나', 1); // 생성자가 Object(this.name, this.num) 이므로 필드 Type에 맞게 입력(String, int)
      // 생성자에 따라 생성된 인스턴스의 필드값 확인
     print(object.name); // 출력 결과 : 나 
     print(object.num); // 출력 결과 :  1
     object.study(); // 출력 결과 : 공부합니다.

     // 필드 type이 const/final가 아니면, 인스턴스의 필드값 재변경 가능
     object.name = '김하준';
     object.num = 5;
     print(object.name); // 출력 결과 : 김하준
     print(object.num); // 출력 결과 : 5
     }
     ```

3. ```static``` 문법 : Class 내에서 정적(static) 필드를 정의할 때 사용
   
   a. 정적 필드/메소드 정의
     - sNum 필드와 func() 메소드 의 type 앞에 static을 추가하였다.
       ```dart
       class Object {
       static int sNum = 0; // 정적 필드
       String name;
       int num;
      
       // 정적 메소드
       static void func() {
         print('안녕하세요');
       }
      
       // 생성자
       Object(this.name, this.num);
       }
       ```

   b. 정적 필드/메소드 호출
   - ```static``` 으로 정의된 필드/메소드는 인스턴스를 생성하지 않고 다음과 같이 접근 가능 ```클래스명.필드명();```
     ```dart
      // 기본적으로 (static이 아닌) 필드/메소드 는 인스턴스 생성 후에 접근 가능
      // Object object = Object();
      // print(object.num); // 필드 값 출력
      ```

      ```dart
      // static인 필드/메소드 는 클래스명으로 바로 접근 가능
      void main() {
      print(Object.sNum); // 필드 값 출력 : 0
      Object.func(); // 메소드 사용 : 안녕하세요
      }
      ```

5. 생성자 사용 시 주요 문법 : Named Parameter
   - **생성자에 { }를 사용하면 선택(Optional 혹은 Named) Parameter이다.**
   - **데이터 타입이 Null을 허용하지 않으면 required를 붙여야 한다.**
   - **타입 뒤에 ```?```을 붙이면 ```Nullable```(Null을 허용)이 된다.**
   - **필수 parameter와 선택 parameter를 동시에 사용할 경우, 필수 parameter가 앞에 와야한다.**
     ```dart
     class Object {
     String name; // Null 허용 X -> required
     int num; // Null 허용 X -> required
     String? field; // Null 허용
    
     // Object(this.name, this.num, this.field); // 생성자 기본 문법
     // 생성자에 Named Paramter 적용
     Object({required this.name, required this.num, this.field}); // (required가 붙은) name, num이 field보다 앞에 와야 한다.
     }
     ```
     
   - 생성자가 Named Parameter인 경우, 인스턴스 생성시 ```named : value``` 형식으로 생성자를 불러와야 한다.
     ```dart
     void main() {
     Object object = Object(name:'하준', num:5); // 'name', 'num'은 필수로 입력하여야 한다. (required)
     Object object = Object(name:'하준'); // 그렇지 않으면 컴파일 에러
     Object object = Object(num:5); // 그렇지 않으면 컴파일 에러
     Object object = Object(); // 그렇지 않으면 컴파일 에러
     }
     ```

  
### Dart 테스트코드 작성
  1. 테스트하고자 하는 파일을 고른다 (lib/파일명.dart)
  2. test 디렉토리 아래 동일 위치에 _test를 붙인 파일을 작성한다. (test/파일명_test.dart)
  3. 여러가지 테스트 기법 중 given > when > then 기법을 사용한다. (*더 공부 필요*)


  
### 객체지향 4가지 특성
1. 캡슐화
2. 상속(계승)
3. 추상화
4. 다형성

  
#### 1. 캡슐화
  - 캡슐화의 개요
    - 캡슐화를 하여 멤버나 클래스로서의 접근을 제어하기 위함
    - 필드에 현실세계에서 불가능한 값이 들어가지 않도록 제어
  - 멤버에 대한 접근 지정
    - private 멤버는 동일 파일내에서만 접근 가능. (**변수 앞에  **_** 을 선언**)
    - public 멤버는 모든 클래스에서 접근 가능 (**디폴트**)
  - 함수, 변수와 동일한 방식으로 클래스에 대한 접근 지정도 할 수 있음.

  
#### 2. 상속(계승)
  - 상속 관계에 따른 클래스 명칭
    - SuperClass : 상위 클래스
    - SubClass : 하위 클래스
  
  - ```SubClas is a SuperClass``` 처럼 ```하위클래스 is a 상위클래스``` 관계가 되어야 한다.
    - 해석 : 하위클래스는 상위클래스의 일종이다. ```예 : 체어맨(하위클래스)은 자동차(상위클래스)의 일종이다.```
  
  - 상속 문법 (추가 예정..)
    - 클래스 상속 관계 표시 : SuperClass가 존재할 때, 상속받아 작성하는 SubClass는 다음과 같이 정의한다. ```class SubClass extends SuperClass```
      ```dart
      class SuperClass {...} 
      class SubClass extends SuperClass {} 
      ```
    - 메소드 오버라이드 : 자식클래스와 부모클래스와 같은 메소드명을 사용할때, 자식클래스에서 메소드 기능을 덮어 쓰는 것 ```@overide``` 으로 주석처리
  
  - UML 다이어그램 : 클래스 간 관계를 표시할 때 사용. [(참고)](https://pdf.plantuml.net/PlantUML_Language_Reference_Guide_ko.pdf)
    - 

#### 3. 추상화
  - 추상 클래스(abstract calss)
    - 목적 : 실제 인스턴스화를 시키지 않으나, 이를 상속받는 클래스에 제공할 필드나 메소드를 모아놓기 위해서 사용 ```abstract class```로 선언
    - 용례 : 내용이 정의되지 않고 상세정의가 미정인 메소드가 있는 클래스에 abstract을 붙여서 사용
    - 제약 : 추상 클래스는 인스턴스화가 금지되어 있다.
    - 
      ```dart
      abstract class Character {
        String name;
        int hp;

      Character(this.name, this.hp);

      // 추상 메소드
      void attack(Slime slime);
      }
      ```
  
  - 인터페이스(interface)
    - 개념 : **추상 클래스 중, 추상메소드만 가지고 있는 것을 인터페이스**로 특별히 취급한다. (interface 키워드는 Dart3에 추가되었음.)

    - **필요조건**
      1. **모든 메소드는 추상 메소드여야 한다**
      2. **필드를 가지지 않는다.**
         
    - 효과
      1. 같은 인터페이스를 구현한 클래스들은 공통 메소드를 구현하고 있음을 보장
      2. 어떤 클래스가 인터페이스를 구현하고 있다면, 적어도 그 인터페이스에 정의된 메소드를 가지고 있다는 것이 보증된다.
      **요약 : 클래스를 통해 인터페이스를 구현하면, 그 클래스는 인터페이스의 메소드를 가지고 있다.**

    - 인터페이스 사용
      - 인터페이스를 부모로 두는 자식 클래스 정의에 implements 를 사용
        ```dart
        abstract class Gender {
        String? name;
        void genericMessage();
        }

        class Man implements Gender {
        @override
        String? name = 'MAN'; 
      
        @override
        void genericMessage() {
          print('I have a mustache');
          }
        }
        ```  
    
