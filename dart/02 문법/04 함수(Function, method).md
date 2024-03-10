함수(Function)
=============
## 함수(Function, Method)란?   
- 프로그램에서 반복해서 사용되는 코드를 하나로 묶어놓은 것이다.        
- 다양한 형태로 존재하며, 필요할 때마다 호출하여 해당 작업을 수행한다.  
- dart는 일급객체를 지원하는 언어이기 때문에 함수를 다른 데이터 유형과 마찬가지로 처리할 수 있다.
<br/>

## 일급객체(first class object)란?  
- 다른 객체들에 일반적으로 적용할 수 있는 연산을 모두 지원하는 객체이다.  
- 다른 함수의 매개변수로 전달할 수 있고, 다른 함수의 매개변수로 전달할 수 있다.  
- 함수를 가지고 연산, 대입 등 변수로 할 수 있던 것을 모두 할 수 있다.  
```dart
void main () {
// 함수 실행 값을 변수에 대입  
int addResult = add(5, 3); 
int sumResult = sum(2, 2);

// 함수로 연산이 가능  
int test = add(3, 2) + sum(4, 3);

// 다른 함수의 매개변수 값으로 전달 가능    
int test2 = add(sum(1, 2), add(3, 2));  

print(addResult); // 8 출력
print(sumResult); // 4 출력
print(test); // 17 출력
print(test2); // 7 출력
}

// 두 수를 더하는 함수
int add(int a, int b) {
return a + b;
}

// 두 수를 곱하는 합수
int sum(int a, int b) {
return a * b;
}
```
<br/>

## 메소드(method)란?   
- 메소드(method)는 클래스에 포함되는 함수이다.  
- 클래스의 동작에 해당한다.
```dart  
class 클래스명 {
    public void 메소드명() { // 메소드명은 camel case 표기
    print('Hello, method');
 }
}
```
<br/>

## 함수의 구성 요소
 ```dart
 int point(int x) { ... }
 // 리턴타입 함수이름(매개변수_데이터타입 매개변수이름) { 반환 값... }
 ```  
 - 리턴타입: void, int, String...     
 - 함수이름: 카멜 표기법(Camel Case)   
 - 매개변수_데이터타입: 함수에 전달되는 매개변수의 데이터 타입   
 - 매개변수이름: 함수에 전달되는 값의 이름   
 - 반환 값: 리턴타입과 일치, 함수가 실행된 후 반환되는 값, 함수가 반환하는 값이 없다면 return;을 사용   
<br/>

## 함수의 정의와 호출방법
### 함수 정의
 ```dart
 int sum(int a, int b) {
   return a + b;
 ```  
<br/>

### 함수 호출   
 ```dart
 int result = add(3, 5);
 print(result); // 8 출력
 ```  
<br/>

## 다양한 형태의 함수
### main 함수    
```dart
void main() {} 
```
- 리턴 값이 없는 void 함수이다.    
- 프로그램의 진입점으로 사용된다. (실행 시 필수)  
- 프로그램이 실행될 때 운영 체제나 런타임 환경은 main 함수를 찾아서 거기서부터 코드를 실행한다.
<br/>

### void 함수
```dart
void main() {} 
```
- 작업을 완료한 후에 값을 반환하지 않을 때 사용된다.  
- 주로 메시지를 출력하는 print 함수가 대표적인 void 함수이다.  
<br/>

### print 함수    
```dart
print('Hello, Dart!');
```
- 반환값이 void인 대표적 함수이다.    
<br/>

### arrow 함수    
 ```dart
   int add(int a, int b) {   
      return a + b;   
   }
   
   int add(int a, int b) => a + b;
 ```
 - 위의 두 코드는 동일한 코드이다.  
<br/>
