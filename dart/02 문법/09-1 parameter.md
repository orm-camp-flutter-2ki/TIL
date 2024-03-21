# 매개변수, 인자 (parameter, argument)
## 생성자란
- 인스턴스를 생성하는 방법을 제공한다.
- 클래스와 동일한 이름을 가지는 함수를 만들어 생성자를 선언할 수 있다.  
<br/>

## named parameter
`name ㅇ` `필수 X` `순서 X` `기본 값 가능`
- `{}`를 사용하여 파라미터에 이름을 붙이도록 강제한다.
- 값이 초기화가 되어있거나, 기본 값을 주거나, nullable `?` 을 붙이면 된다.  
```dart
double xPoint; 
double? yPoint; 

Point({this.xPoint = 0, this.yPoint});
```
<br/>

## optional positional parameter
`name X` `필수 X` `순서 ㅇ` `기본 값 가능`
- `[]`를 사용하여 위치를 지정하는 파라미터이다.
- 기본 값을 주거나, nullable `?` 을 붙이면 된다.  
```dart
double xPoint; // x 좌표
double yPoint; // y 좌표

Point(this.xPoint, [this.yPoint = 0]);
```
<br/>

## named required parameter  
`name ㅇ` `필수 ㅇ` `순서 X` `기본 값 불가능` 'nullable 가능`
- `required` 키워드를 붙여 강제한다.
```dart
double xPoint; // x 좌표
double yPoint; // y 좌표

Point({required this.xPoint, required this.yPoint});
```
<br/>
