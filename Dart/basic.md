## [Dart 기초]

### 객체 지향 프로그래밍, OOP
- 오브젝트(객체) : 현실 세계의 모든 객체 : **상태(속성)과 동작으로 구성**
- 클래스 : 객체를 가상세계 용으로 구체화한 것 : **필드와 메소드**
  - 클래스를 정의하면, 그 클래스 타입의 변수를 선언할 수 있다.(String type도 클래스(레퍼런스 타입)이다.)
- 인스턴스 : 클래스가 컴퓨터 Heap 메모리에 할당된 상태 (**인스턴스는 ```생성자```를 통해 생성됨**)

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
     }
     // 메소드
     void study() {}
     ```

  
2. 인스턴스 생성
   - 클래스명 Object가 선언되어있을 때, 인스턴스는 다음과 같이 생성한다. ```클래스명 인스턴스명 = 클래스명(생성자)```
     ```dart
     // Object object = new Object() // Dart에서는 우항의 생성자 생성을 위한 new 문법이 불필요하다.
     Object object = Object() // 즉, new를 생략하고 인스턴스를 생성한다. 
     ```
   - 생성자 인스턴스 필드에 대한 접근은 ```.``` 을 이용한다.
     ```
     void main() {
     Object object = Object('나', 1); // 생성자가 Object(this.name, this.num) 이므로 필드 Type에 맞게 입력(String, int)
     // 생성자에 따라 생성된 인스턴스의 필드값 확인
     object.name;
     object.num;
     // 필드 type이 const/final가 아니면, 인스턴스의 필드값 재변경 가능
     object.name = '김하준';
     object.num = 5;
     object.study(); // 메소드 동작
     }
     ```

3. ```static``` 문법 : Class 내에서 정적(static) 필드를 정의할 때 사용
   
   a. 정적 필드/메소드 정의
   ```dart
    class Object {
    static int sNum = 0; // 정적 필드
    String name;
    int num;

    static void func() { ... } // 정적 메소드
    ```

   b. 정적 필드/메소드 호출
   - ```static``` 으로 정의된 필드/메소드는 인스턴스를 생성하지 않고 다음과 같이 접근 가능 ```클래스명.필드명();```
     ```dart
     void main() {
      // (static이 아닌) 기본적으로 필드/메소드 는 인스턴스 생성 후에 접근 가능
      // Object object = Object();
      // object.func();
    
      // static인 필드/메소드 는 클래스명으로 바로 접근 가능
      Object.func();  
      print(Object.sNum);
      }
      ```

4. 생성자 사용 시 주요 문법 (수정 중)
   - **타입 뒤에 ```?```을 붙이면 ```Nullable```이 된다.**
   - **데이터 타입이 Null을 허용하지 않으면 required를 붙여야 한다.**
     ```dart
     class Object {
     String name; // Null 허용 X -> required
     int num; // Null 허용 X -> required
     Field? field; // Null 허용
    
     // Object(this.name, this.num, this.field);
     Object(required this.name, required this.num, this.field);
     }
    ```
    ```dart
    void main() {
    Object object = Object('하준', 5); // 위의 생성자 문법에 따라, 'name', 'num'은 필수로 입력하여야 한다. (required)
    // Object object = Object('하준'); // 그렇지 않으면 컴파일 에러
    // Object object = Object(5); // 그렇지 않으면 컴파일 에러
    // Object object = Object(); // 그렇지 않으면 컴파일 에러
    }
    ```
  
- **생성자에 { }를 사용하면 선택(Optional 혹은 Named) Parameter이다.**
  - **필수 parameter와 선택 parameter를 동시에 사용할 경우, 필수 parameter가 앞에 와야한다.**
    ```dart
    class Object {
    String name;
    int num;
    Field? field; // Named Parameter
    
    Object(this.name, this.num, {this.field});
    ```
  - Named Parameter인 경우, ```named : value``` 형식으로 생성자를 생성하여야 한다.
    ```dart
    void main() {
    Object object = Object('김하준', 5, field:'필드'} //
    }
    ```

### Dart 테스트코드 작성
  1. 테스트하고자 하는 파일을 고른다 (lib/파일명.dart)
  2. test 디렉토리 아래 동일 위치에 _test를 붙인 파일을 작성한다. (파일명_test.dart)
  3. 여러가지 테스트 기법 중 given > when > then 기법을 사용한다.

### 객체지향 4가지 특성
1. 캡슐화
2. 상속(계승)
3. 다형성
4. 추상화
   
### 캡슐화
  - 캡슐화의 개요
    - 캡슐화를 하여 멤버나 클래스로서의 접근을 제어하기 위함
    - 필드에 현실세계에서 불가능한 값이 들어가지 않도록 제어
  - 멤버에 대한 접근 지정
    - private 멤버는 동일 파일내에서만 접근 가능. (**변수 앞에  **_** 을 선언**)
    - public 멤버는 모든 클래스에서 접근 가능 (**디폴트**)
  - 함수, 변수와 동일한 방식으로 클래스에 대한 접근 지정도 할 수 있음.

### 상속(계승)
  - 상속 관계에 따른 클래스 명칭
    - SuperClass : 상위 클래스
    - SubClass : 하위 클래스
  - ```SubClas is a SuperClass``` 처럼 ```하위클래스 is a 상위클래스``` 관계가 되어야 한다.
    - 해석 : 하위클래스는 상위클래스의 일종이다. ```예 : 체어맨(하위클래스)은 자동차(상위클래스)의 일종이다.```
  - 상속 문법
    - SuperClass가 정의되어 있을 때, 상속받는 SubClass는 다음과 같은 문법으로 정의한다.
      ```class SubClass extends SuperClass```
      
      ```dart
      class SuperClass {...} 
      class SubClass extends SuperClass {} 
      ```
      
  - UML 다이어그램 : 클래스 간 관계를 표시할 때 사용. [(참고)](https://pdf.plantuml.net/PlantUML_Language_Reference_Guide_ko.pdf)
  
  - 오버라이딩 : 자식클래스와 부모클래스와 같은 메소드명을 사용할때, 자식클래스에서 메소드 기능을 덮어 쓰는 것 ```@overide```
    - (예시 코드추가 예정)
