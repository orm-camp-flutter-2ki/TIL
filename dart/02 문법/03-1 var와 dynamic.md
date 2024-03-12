# 타입 추론 var, dynamic
- 모든 타입을 받을 수 있다는 공통점이 있다.
- 할당되는 값에 따라 타입을 추론한다.   
<br/>

## var
- 컴파일 타임에 타입이 결정되는 키워드이다.  
- 초기화된 값에 따라 타입이 결정된다.
- 함수나 메소드 내부에서 지역 변수를 선언할 때 관습적으로 사용한다.  
- 클래스에서 변수나 property를 명시적으로 나타낼 때 사용한다.   
<br/>

### var 초기화 시점에 따른 타입
- 선언 후 값을 할당했을 경우 var는 dynamic으로 선언된다.
```dart
// 선언과 동시에 초기화
  var number = 10; // int로 선언됨
  number = '10'; // type error
  number = true; // type error
  
// 선언 후 초기화
  var name; // dynamic으로 선언됨
  name = 1034.3; // not error
  name = false; // not error
```
<br/>

## dynamic  
- 사용하지 않는 것이 좋다.  
- 런타임에 타입이 결정되는 키워드이다.  
- 동적으로 값에 따라 타입이 결정된다.

```dart
  dynamic name = 10; // int로 선언됨
  name = 1034.3; // not error
  name = false; // not error
```
<br/>

- 타입을 아직 알 수 없는 경우에 사용하며, 타입지정 전까지는 제한된 메소드를 사용한다.    
```dart
void main() {
  dynamic name;

  // 타입이 불확실해 제한된 메소드 사용
  print(name.toString());
  print(name.runtimeType);
  
  // 타입 정해지면 타입에 대한 메소드를 사용
  if (name is String) {
    name.isNotEmpty;
    name.length;
  }
  
  if (name is int) {
    name.isOdd;
    name.isEven;
  }

}
```
<br/>
