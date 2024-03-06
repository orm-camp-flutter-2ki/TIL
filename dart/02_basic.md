## Dart 기초 문법

### 1. Variables 변수
- 타입을 지정하지 않고 var를 사용하여 선언할 수 있다. var는 null값을 가질 수 있음.
- 변수는 선언과 초기화가 필요하다.
- Null-safety가 중요하기 때문에 null을 허용하지 않는 변수를 사용하는 경우 반드시 그 값을 초기화해야 한다.

```dart
void main() {
  // 정수형 변수
  int number = 42;
  
  // 실수형 변수
  double pi = 3.14;
  
  // 정수 실수 둘다 가능한 변수;
  num c = 1; 

  // 불리언 변수
  bool isDartFun = true;
  
  // 문자열 변수
  String greeting = 'Hello, Dart!';
  
  // 리스트 변수
  List<int> numbers = [1, 2, 3, 4, 5];
  
  // 맵 변수
  Map<String, int> ages = {
    'Alice': 25,
    'Bob': 30,
    'Charlie': 35,
  };
```
#### Late
 - 값을 선언하고 초기화를 안했지만 언젠가는 값을 할당할때 쓴다. <br/>
#### final / const
- final : 초기화 후에 값을 변경할 수 없음 (컴파일 타임)
- const : 값을 변경할 수 없음 (런타임)

#### 컴파일 타임 vs 런타임

- 컴파일 시간: 개발자가 코드를 컴파일하는 시간

- 런타임: 사용자가 소프트웨어를 실행하는 시간.

- 즉, 현재 컴파일 타임이 현재에 가깝고 런타임이 나중이다.

```
  //DateTime, 시간과 날짜를 저장할수있는 데이터타입

  //final 가능.
  final DateTime now = DateTime.now(); 
  print(now);
  
  //const 불가능. 빌드타임을 모르기때문
  //const DateTime now2 = DateTime.now(); 
  //print(now2);
```
### 2. Control Flow 제어문
- 제어문에는 if/else, switch/case, while, do/while, for in 등이 포함된다.
```dart
// switch-case 문: 다중 분기 처리
String fruit = 'apple';
  switch (fruit) {
    case 'apple':
      print('This is an apple');
      break;
    case 'banana':
      print('This is a banana');
      break;
    default:
      print('This is not a fruit');
  }

 //while문
  int count = 0;
  while (count < 5) {
    print(count);
    count++;
  }

 // do-while 문: 코드를 최소한 한번 실행하고, 조건이 참인 동안 반복 실행
  int i = 0;
  do {
    print(i);
    i++;
  } while (i < 3);
}

  // for-in 문: 리스트나 맵의 모든 항목에 대해 반복
  List<int> numbers = [1, 2, 3, 4, 5];
  for (int number in numbers) {
    print(number);
  }
```
### 3. Functions 함수
- 함수는 특수한 입력값과 반환하는 값의 타입을 지정해주는것이 권장된다. 
- void는 타입과 반환값을 지정하지 않는다. 
- 함수가 다른 함수의 인수로 사용될 수도 있다. 
- 인수값만 다르지만 목적이 같은 기능을 만들때 쓴다. 
