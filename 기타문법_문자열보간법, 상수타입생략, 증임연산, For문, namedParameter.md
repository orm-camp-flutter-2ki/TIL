# 기타문법
## 문자열보간법
```dart
String _name = '홍길동';
int _age = 8;

print('$_name은 $_age살입니다');
```

## 상수의 타입 생략 가능
```dart
final String greeting1 = '안뇽';
final numberA = 3;

const String greeting2 = '하이';
const numberB = 5;
```


## 증임연산자
```dart
int num = 0;

print(num++); // 0 (출력 이후에 1이 증가함)
num += 1
print(++num); // 2 (출력 전에 1이 증가함)
```

## For문의 사용
```dart
for (초기식; 조건식; 증감식) {
    실행문;
}
```

```dart
//dart

for(int i = 1; i <= 9; i++) {
    // i를 지역변수로 활용가능
    // 실행구문
 }
 
 // swift
 
 for i in 1...9 {
    // i를 지역변수로 활용가능
    // 실행구문
}
```

```dart
// dart

List<String> items = ['item0', 'item1', 'item3']
for (String item in items) {
    // item 지역변수로 활용가능
    // 실행구문
}

// swift

var items: [String] = ["item0", "item1", "item2"]
for item in items {
    // item 지역변수로 활용가능
    // 실행구문
}
```
- 형태가 달라서 조금 헷갈리는 면이 있었다.
- 틈나면 사용해서 익숙해지도록하자

## named Parameter
```dart
void something({int age = 10, String name = '', String hobby: ''}) { ... }

// 사용예시
something(age: 10, name: '안뇽'); // 초기값을 무조건 세팅해야하므로 입력인자 선택가능
something(name: '하위', age: '50', hobby: '트래킹'); // 순서변경가능
something();
```
