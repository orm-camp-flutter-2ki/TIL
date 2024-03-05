Dart 기초
=============
### 목차  
1. 데이터타입(Data Type)  
2. Dart에 있는 중요한 차이점    
3. 함수(Function, Method)    

<br/>

## 데이터타입(Data Type)  

### int: 정수형  
> ```
> int age = 10;
> ```

### double: 실수형  
> ```
> double PI = 3.14;
> ```

### String: 문자열  
> ```
> String name = 'myName'; // 큰 따옴표도 가능하지만, 작은 따옴표가 표준
> ```

### bool: 참-거짓(bloolea, true-false)  
> ```
> bool isClean = false;
> ```

### List: 순서가 있는 변수들의 집합
> ```
> // 생성과 함께 초기화
> List<int> numbers = [1, 2, 3, 4, 5];
>
> // 리스트에 값, 요소, 데이터, 변수 추가
> numbers.add(6);
>
> // 리스트의 특정 인덱스에 접근
> int firstNumber = numbers[3]; // 4;
>
> // 리스트의 길이 확인
> int M = numbers.length; // M == 6
>
> // 리스트 출력
> print(numbers); // 출력 결과: [1, 2, 3, 4, 5, 6]
> ```
>✔️ 순서(Index)가 있음 (0부터 시작)  
>✔️ 같은 리스트 내 다양한 데이터 타입 포함 가능   
>✔️ 필요에 따라 항목을 추가하거나 삭제 가능  

### Map: 키-값의 쌍 (key-valued)  
> ```
> // 이름(key)과 나이(value)를 매핑
> Map<String, int> person = {
>   'John': 30,
>   'Alice': 25,
> };
>
> // 요소 추가
> person['Bob'] = 35; // 'Bob' 추가
>
> // 요소 제거
> person.remove('Alice'); // 'Alice' 삭제
>
> // 맵의 모든 요소 제거
> person.clear();
>
> // 특정 키의 값
> int johnAge = person['John'];
>
> // 모든 키값
> Set<String> keys = person.keys;
> ```
>✔️ 키에 해당하는 값, 특정 키를 사용하여 해당하는 값을 가져옴



<br/>

## Dart에 있는 중요한 차이점  

### var: 데이터 타입 추론 (Variables)  
> ```
> var num = 4; // int
> num = 6; // 가능
> num = '고양이'; // 불가능, error
> ```
>✔️ 변수의 타입은 초기 값에 따라 결정  
>✔️ 데이터 타입 변경 불가, 컴파일 타임 기준으로 결정되기 때문 (값은 재선언 가능)  
>✔️ 코드의 가독성이 떨어질 수 있음, 명시적으로 데이터 타입 지정하는 것이 좋음  

### Null safety: 널 세이프티  
>✔️ 널 포인터(null pointer) 예외를 방지하고 안전한 널 처리(null handling)를 보장  
>✔️ 널 포인터(null pointer): 메모리 내에서 아무런 주소를 가리키지 않는 포인터를 가리키는 것  
>✔️ 널 처리(null handling): 프로그램에서 널 값을 다루는 방법   

### nullable: 널러블
> ```
> String? name = null; // null
> String? name; // null
>
> String name = null; // 불가능, error
> String name; // 불가능, error.. but 나중에 재선언으로 값 할당 하니까 선언부의 빨간줄 없어짐..
> ```
>✔️ null 값을 허용하는 변수  
>✔️ 데이터타입 뒤 ? 를 붙여 선언, null값을 가질 수 있음을 명시적으로 표현  
>✔️ 코드 안정성 높아짐 (널 세이프티)  

<br/>

## 함수(Function, Method)   
### main 함수    
>✔️ 프로그램의 진입점으로 사용 (실행 시 필수)  
>✔️ 프로그램이 실행될 때 운영 체제나 런타임 환경은 main 함수를 찾아서 거기서부터 코드를 실행  

<br/>

### Control Flow 제어문
**반복문**
>✔️ for (주어진 범위가 있을 경우 그 안에서 반복 실행)    
>✔️ while (loop문, 조건이 참일 경우 반복 실행)  
>✔️ do/while (무조건 한번 실행 후 조건의 참-거짓 판단, 잘 사용하지 않음, while 사용..)   

**조건문**
>✔️ if/else (특정 조건의 true-false 여부에 따라 실행)   
>✔️ swhich/case(특정 값의 일치 여부에 따라 실행)    

<br/>

### Functions 함수(메소드)    
> ```
>   int add(int a, int b) {   
>      return a + b;   
>   }
>   
>   int add(int a, int b) => a + b;
> 
>   두 코드는 동일함
> ```
>✔️ 매개 변수와 리턴(return)의 타입을 지정해주는 것을 권장  
>✔️ 리턴값 없는 void 함수 (ex. main 함수)   
>✔️ 화살표 함수(arrow function) =>(화살표) 단축 구문 사용 가능  



