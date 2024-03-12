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

### Dart 테스트코드 작성
  1. 테스트하고자 하는 파일을 고른다 (lib/파일명.dart)
  2. test 디렉토리 아래 동일 위치에 _test를 붙인 파일을 작성한다. (파일명_test.dart)
  3. 여러가지 테스트 기법 중 given > when > then 기법을 사용한다.
   
### 캡슐화
  - 캡슐화의 개요
    - 캡슐화를 하여 멤버나 클래스로서의 접근을 제어하기 위함
    - 필드에 현실세계에서 불가능한 값이 들어가지 않도록 제어
  - 멤버에 대한 접근 지정
    - private 멤버는 동일 파일내에서만 접근 가능. (**변수 앞에  **_** 을 선언**)
    - public 멤버는 모든 클래스에서 접근 가능 (**디폴트**)
  - 함수, 변수와 동일한 방식으로 클래스에 대한 접근 지정도 할 수 있음.
