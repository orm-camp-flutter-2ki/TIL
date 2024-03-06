## 형상관리

- 형상관리란: 소스 변화 관리 툴
- 도구 종류:  Git, SVN,  CVS

---

# [Dart]

-객체지향 및 함수형 프로그래밍 지원.

-변수 선언: var

## 기본 자료형

-int: 정수

-double: 실수(소수점)

-String: 문자열

-bool: 참 또는 거짓 값을 갖는 타입(불리언타입)

## 문자열

-작은 따옴표가 표준임.

## 문자열 포맷
```
String _name = '홍길동';
int _age = 20;

void main(){
 print('$_name은 $_age살입니다.');
 print('$_name은 ${_name.length} 글자입니다.');
 print('10년 후에는 ${_age + 10}살입니다.');
}
```

## 숫자

-정수 (int)
-실수 (double)
-숫자 (num)

## 숫자 타입의 포함관계

```dart
int a = 10;
double b=a; // 에러
교집합이 없음. 

일부 언어에서는 더 큰 자료형인 double 타입에 int 타입을
대입하는 자동 형변환을 지원하기도 하지만 다트에서는 지원하지 않음

```

## 상수

final 키워드를 사용. 타입을 생략해도 됨.

```dart
final String name = '홍길동
name = '임꺽정'; // 에러

```

## 산술연산자

+더하기, -빼기, *곱하기, /나누기(double 타입 반환) / ~/몫(int 타입 반환) / 

```dart
ex)
print(5 /2 );   // 2.5 처럼 double이 나옴.
```

- 함수에는 ( )의 형태를 가짐. ex) print (값);


```
void main() {
  print(isEven(10));
  print(isEven(5)); 
}

bool isEven(int num) {
  if (num %2 ==1){
    return true;
  }
  return false;
}
//홀짝 구하기
```

## 증감 연산자 (++)

```dart
var num = 0;
print(num++); // 나중에 계산하므로 0출력 // num = 1이 됨
print(++num); // 먼저 계산하므로 2출력 // num=2가 됨
```

## 비교 연산자

==같다 !=다르다, >더크다, <더작다, ≥크거나 작다, ≤작거나크다

```dart
ex) 
```

## 논리 연산자

&&그리고

|| 또는

! 부정

! = 다르다

```dart
ex)
  print((10%2 ==0)&& true);  // true
```

## 타입검사

is: 같은 타입이면 true

is!: 다른 타입이면 true

```dart
int a = 10;
if (a is int) {
 print('정수');
}
```

## 형변환

- 명시적: as 사용   ⇒ 위험함. 쓰지 않는것이 좋음..!
- 암시적: 포함관계일 경우 as 생략 가능

## 삼항연산 활용 분기
 ```dart
 bool isRainy = true;
  if (isRainy){
    print('빨래를 안 한다');
  }else {
    print('빨래를 한다');
  }  } //빨래를 안 한다

-----
void main() {
  bool isRainy = true; // 비가 오는지 여부를 나타내는 변수
  
  String result = ' '; // 결과를 저장할 변수
  
  // if-else 문을 사용하여 비가 오는지 여부에 따라 결과를 설정합니다.
  if (isRainy) {
    result = '빨래를 안 한다';
  } else {
    result = '빨래를 한다';
  }
  
  print(result); // 결과를 출력합니다.
  
  // 삼항 연산자를 사용하여 같은 작업을 수행합니다.
  result = isRainy ? '빨래를 안 한다' : '빨래를 한다';
  
  print(result); // 변경된 결과를 출력합니다.
}

```

## switch case

열거형(enum)과 함께 사용시 모든 케이스 검사 강제성이 생김

사람의 실수를 미연에 방지 가능

```dart
true, false 이외에 값 가지고 분기문을 활용할때 사용함.

```

## import

-print 이외에 사용. 내장 라이브러리를 사용하겠다고 선언할 때

(stdin.readLineSync() 이런 코드 사용할 때 자동으로 입력 됨.)

### FOR문

```dart
void main() {
for(변수초기화 ; 조건; 변수조작){
  [print('!!!!')]
}

----
for (int i = 0; **i<3**; i++){
print('!!!!');
//for 반복문은 주어진 조건에 따라 코드 블록을 여러 번 반복함.
여기서는 int i = 0으로 시작해서 i가 3보다 작을 때까지 반복합니다. i를 1씩 증가시킵니다.

---
void main() {
  var items = ['짜장', '라면', '볶음밥'];
  for(var i = 0; i < items.length; i++) {
    print(items[i]);
  }
}

* i<items.lenghth 는 반복문의 조건 부분으로, 리스트 items의 길이보다 작을 때까지 반복함
* print(items[i]); = [i]를 넣는것은 인덱스를 사용할 때 씀.

//forEach 문은 없고, 무지성 뺑뺑이
for(String item in items){
print(item);
}
}
```

---


## 컴파일언어(자바스크립트) vs 인터프리트 언어(다트)

-컴파일 언어: 자바스크립트 언어

-인터프리트 언어: 타입이 안전해 한번 결정되면 변경되지 않음. 중간에 통역사 역할을 해주는 인터프리터라는 것이 0과 1을 사용해서 프로그래밍 언어를 실시간으로 번역하는 것.


### named 매개변수(parameter)

-매개변수: 함수를 정의할 때 사용되는 변수(variable)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/11384fea-4fca-4f31-b6f2-8d8a89612cb0/29533987-d902-465a-bb2f-adbd809800cd/Untitled.png)

```dart
void something({String name, int age = 10}) {
               
void main(){
 something(name: '홍길동', age: 10);
 something(name: '홍길동');     
}
```

---

## final vs const

- 둘 다 상수 선언 키워드임(⇒ 일단 파이널로 쓰고, 플러터 사용 때 const 쓰기)

-final: 런타임 시점에 값이 할당되어 상수가 됨. 매번 메모리 사용

-const: 컴파일 시점에 값이 할당되어 상수가 됨. 메모리 아끼고 효율 증가.

---

### - 코드 정리 단축키

ctrl+Alt+L

### - 컴파일

컴퓨터가 이해하는 언어로 바뀌는 것.

컴퓨터는 1, 0만 인식함. 그래서 컴파일을 거침(ex. 다트 언어로 써주면 번역해서 실행하는 것)

번역 돌리는 도중에 잘못되는 것을 실행 전에 미리 알려주는 것을 컴파일 에러라고 함.

### - 런타임
실행을 해봐야 알 수 있는 에러를 런타임 에러라고 함.
