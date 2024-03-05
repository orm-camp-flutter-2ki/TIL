
## 변수(Variables)

- 값을 저장하고 참조할 때 사용하는 중요한 개념
- 변수는 선언과 초기화가 필요함
- 변수는 타입이 필요함
- type-safe를 유지하면서도 대부분의 변수에 타입을 지정하지 않고 var를 사용하여 선언할 수 있음. 변수 타입은 초기값에 따라 결정

```dart
ex)
var name = "bob";

```

## Operators

수학적인 연산이나 비교, 논리 등의 기능을 수행하는 기호나 키워드


## 주석(Comments)

한 줄 주석, 문서화용 주석 등

( //는 한줄주석, ///는 라이브러리, 클래스 등)

## 

## 함수(Functions)

함수는 특수한 경우를 제외하고 인수(넣어주는 값)와 반환하는 값의 타입을 지정

type이 void면 값을 반환하지 않기 때문에 반환 값을 지정하지 않아도 됨.

```dart
void main() {
    // 타입 지정된 함수
    int add(int a, int b) {
        return a + b;
    }  

--
void main(){
  int result = add(5, 3); 
  print('5+3=$result');
}
```

간단한 짧은 함수는 =>(화살표) 단축 구문 사용 가능.

```dart
int multiply(int a, int b) => a * b;
```

## 제어문(Control flow)

- if/else = 조건에 따라 코드 실행 여부 결정

```dart
void main(){
int number = 42;
if (number>50) {           // 42 > 5- => true? false
	print('number is greater than 50');
} else {
  print('number is less than or equal to 50');
}
```

- switch/case

```dart
**String fruit = 'apple';      // fruit == apple**
switch (fruit) {
 case 'apple';
   print('this is an apple');
   break;
case 'banana';
   print('this is a banana');
   break;
default;
   print('this is not a fruit');
```

- while: 조건이 참인 동안 코드 반복 실행

```dart
int count = 0;

while (count <5) {
 print(count);
 count++;
}
```

- do/while: 코드를 최소한 한번 실행하고 조건이 참인 동안 반복

```dart
int i = 0;

do {
  print(i);
  i++;
 }while (i <3);
}
```
