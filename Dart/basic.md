# [Dart 기본]

## [객체 지향 프로그래밍, OOP]  

<객체 관련 개념>
  - **a. 오브젝트(객체)** : 현실 세계의 모든 객체 : **상태(속성)과 동작으로 구성**
  - **b. 클래스** : 객체를 가상세계 용으로 구체화한 것 : **필드와 메소드**
    - 클래스를 정의하면, 그 클래스 타입의 변수를 선언할 수 있다.(String type도 클래스(레퍼런스 타입)이다.)
  - **c. 인스턴스** : 클래스가 컴퓨터 내의 Heap 메모리에 할당된 상태 : **인스턴스는 ```생성자```를 통해 생성됨**
    


**1. 클래스 생성**
   - a. 클래스명은 대문자로 시작해야 하고, 클래스가 가지는 필드/메소드를 정의할 수 있다.
     ```dart
     // 클래스
     class Student {
     
        // 필드(멤버변수)
        String name;
        int age;
     
        // 메소드
        void study() {
        print('공부합니다.');
        }
     }
     ```
     - 필드(멤버변수) : 클래스의 특징이나 상태를 표현 (클래스의 인스턴스마다 고유한 값을 가질 수 있음) ```타입 변수명```
     - 메소드 : 클래스 내에서 동작하는 함수 ```반환타입 함수명() {}```

   - b. 생성자를 함께 정의한다.
     ```dart
     // 클래스
     class Student {
        // 필드
        String name;
        int age;
        // 메소드
        void study() {
        print('공부합니다.');
        }
     
        // 생성자
        Student(this.name, this.age);
     }
     ```
     - 생성자 : Student(this.name, this.age) 여기서 ```this```는 현재 클래스(Student)을 의미
     
  
**2. 인스턴스 생성**
   - 클래스가 선언되어있을 때, 인스턴스는 다음과 같이 생성한다. ```클래스명 인스턴스명 = 클래스명(생성자)```
     ```dart
     // Object object = new Object() // Dart에서는 우항의 생성자 생성을 위한 new 문법이 불필요하다.
     Student student = Student() // 즉, new를 생략하고 인스턴스를 생성한다. 
     ```     
   
   - 인스턴스가 가진 필드/메소드 값은 ```인스턴스명.필드명``` 으로 접근할 수 있다.
     ```dart
     print(student.name);
     print(student.age);
     object.study();
     ```
     
   - 1-b에 대한 프로그램 실행(결과)
     ```dart
     void main() {
     Student student = Student('나', 30); // 생성자가 Object(this.name, this.num) 이므로 필드 Type에 맞게 입력(String, int)
      // 생성자에 따라 생성된 인스턴스의 필드값 확인
     print(student.name); // 출력 결과 : 나 
     print(student.age); // 출력 결과 : 30
     student.study(); // 출력 결과 : 공부합니다.

     // 필드 type이 const/final가 아니면, 인스턴스의 필드값 재변경 가능
     student.name = '하준';
     student.age = 28;
     print(student.name); // 출력 결과 : 하준
     print(student.age); // 출력 결과 : 28
     }
     ```

3. ```static``` 문법 : Class 내에서 정적(static) 필드를 정의할 때 사용
   
   a. 정적 필드/메소드 정의
     - sNum 필드와 func() 메소드 의 type 앞에 static을 추가하였다.
       ```dart
       class Student {
         static int sNum = 5; // 정적 필드
         String name;
         int age;
        
         // 정적 메소드
         static void greet() {
           print('안녕하세요');
         }
        
         // 생성자
         Student(this.name, this.age);
         }
       ```

   b. 정적 필드/메소드 호출
   - ```static``` 으로 정의된 필드/메소드는 인스턴스를 생성하지 않고 다음과 같이 접근 가능 ```클래스명.필드명();```
     ```dart
      // 기본적으로 (static이 아닌) 필드/메소드 는 인스턴스 생성 후에 접근 가능
      // Student student = Student();
      // print(student.age); // 필드 값 출력
      ```

      ```dart
      // static인 필드/메소드 는 클래스명으로 바로 접근 가능
      void main() {
      print(Student.sNum); // 필드 값 출력 : 5
      Student.greet(); // 메소드 사용 : 안녕하세요
      }
      ```

4. **생성자 사용 시 주요 문법 : Named Parameter**
   - 생성자() 안에 ```{ }```를 사용하면 선택(Optional 혹은 Named) Parameter이다.
   - 데이터 타입이 Null을 허용하지 않으면 ```required```를 붙여야 한다.
   - 타입 뒤에 ```?```을 붙이면 Nullable(Null을 허용)이 된다.
   - 필수 parameter와 선택 parameter를 동시에 사용할 경우, 필수 parameter가 앞에 와야한다.
     ```dart
     class Object {
     String name; // Null 허용 X -> required
     int age; // Null 허용 X -> required
     String? field; // Null 허용
    
     // Student(this.name, this.age, this.field); // 기본 생성자
     
     // Named Paramter을 받는 생성자
     Student({required this.name, required this.age, this.field}); // (required가 붙은) name, age이 field보다 앞에 와야 한다.
     }
     ```
     
   - 생성자가 Named Parameter인 경우, 인스턴스 생성시 ```named : value``` 형식으로 생성자를 불러와야 한다.
     ```dart
     void main() {
     // Student student = Sbject('하준', 28); // 생성자 값을 Named parameter로 받지 않아 에러
     Student student = Student(name:'하준', age:28); // 'name', 'age'은 필수로 입력하여야 한다. (required)
     // Student student = Student(name:'하준'); // 에러
     // Student student = Student(age:28); // 에러
     // Student student = Student(); // 에러
     }
     ```

---
  
### <객체지향 4가지 특성>
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
    - 개념 : **추상 클래스 중, 추상메소드만 가지고 있는 것을 인터페이스**로 특별히 취급한다.
      (interface 키워드는 Dart3에 추가되었음.)

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

#### 4. 다형성(Polymorphism)
 - 정의 : 객체를 다양한 형태로 볼 수 있는 것 (예: 자동차, 벤츠, 세단, ... 어쨌든 대충보면 자동차다.)
 - 선언 방법 : ```선언을 상위 개념으로 인스턴스 생성은 하위 개념으로 한다.```
   - ```Character character = Hero('홍길동', 100);``` // Character는 Hero의 상위개념
   - 어떤 멤버를 이용할 수 있는 가는 선언부(Character) 타입이 결정한다. (Hero가 아닌 ```Chracter의 메소드만을 사용가능```)
   - 멤버가 어떻게 움직이는지는 인스턴스 생성부(Hero) 타입이 결정한다. (Hero 생성자로 인스턴스화되어 ```character.메소드``` 로 메소드 사용)
  

 - 용례
   - Class를 Interface로 선언
     
     a. Interface 정의
       ```dart
       abstract interface class Drawable {
         void draw();
       }
       ```
       
     b. Interface 구현
       ```dart
       class House implements Drawable {
         void draw() {
          ...
        }
       }
       }
       ```

     c. **Class를 Interface로 선언**
       ```dart
       Drawable element = House(...);
       List<Drawable> elements = [];
       elements.add(Dog(...));
       ```

--- 
