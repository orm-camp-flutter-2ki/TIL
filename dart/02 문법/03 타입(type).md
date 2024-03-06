형, 타입 (Type)
============= 
- 데이터나 변수가 어떤 종류의 값들을 가질 수 있는지를 결정한다.  
<br/>

## 타입 검사  
```dart
 num age = 36;
 print(age.runtimeType); // int 출력
 ```
- .runtimetype 사용하여 타입 검사 
 ```dart
 int age = 10;
 
 if (age is int) {
 print('정수')
 } // 정수 출력

 String name = 'jiyeong';
 
 if (name is! int) {
 print('숫자가 아님')
 } // 숫자가 아님 출력
 ```
- is/is! 사용하여 타입 검사
- is  : 같은 타입이면 true 가 출력된다.  
- is! : 다른 타입이면 true 가 출력된다.  

<br/>

## 형 변환 (Type casting)
### as 형변환
 ```dart
 num age = 14;
 int ageInt = age as int; // 14 출력, type int
 double ageDouble = age as Double; // error
 
 num high = 164.5;
 double highDouble = high as double; // 164.5 출력, type double 
 int highint = high as int; // error
 ```
- 다른 타입 간의 형 변환  
- 강제성이 있다.  
- as 단언문이라 런타임에 에러가 난다.  

### .to 형변환
 ```dart
 int age = 11;
 print(age.toString); // '11' 출력
 ```

### parse() 형 변환

 ```dart
 String numStr = '123';
 int num1 = int.parse(numStr); // 123 출력
 double num2 = double.parse(numStr); // 123.0 출력
 ```

### 문자열 변환
 ```dart
 String numStr = '1, 2, 3, 4, 5';
 List<String> numList = numStr.split(', '); // 문자열을 쉼표_(, ) 기준으로 분할
 print(numList) // [1, 2, 3, 4, 5] 출력
 ```
- 특정 구분자 기준으로 분할하여 변환  
 ```dart
 String text = 'Hello';
 List<String> char = text.split('');
 print(char); // [H, e, l, l, o] 출력
 ```
- 문자열을 문자 단위로 분할하여 변환   

<br/>

