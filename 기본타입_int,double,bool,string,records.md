# Dart의 거의 비슷한 기본타입(int,double,bool,String,Records)
```dart
int numA = 10;
double numB = 1.0;
bool isOn = true;
String text = '안뇽';
```
- 위 타입들은 선언방법을 제외하면 거의 사용법이 비슷한 것으로 보인다.
- String만 대문자로 표기해주는데 이 목적은 Java에서의 사용을 그대로 계승하여 사용자를 더 쉽게 유입시키기 위함이라고 한다

# Dart에서 생소한 기본타입
### Records
```dart
// 1. 타입추론이 가능하도록하는 Variable(변수) 키워드로 선언한 Records
var record = ('first', a: 2, b: true, 'last');

// 2. 타입을 모두 명시해놓은 Records
(int x, int y, int z) point = (1, 2, 3);
(int r, int g, int b) color = (1, 2, 3);

// 3. 변수 선언을 한 유형의 Records (중괄호가 있음)
({int a, bool b}) record; // 선언
record = (a: 123, b: true); //init
```

```dart
(int, int) swap((int, int) record) {
  var (a, b) = record;
  return (b, a);
}
```
- 위 유형을 처음 보고 다소 난해했다. 이게 뭐지? 싶었는데
- 자세히 보고나니 아래와 같은 튜플을 반환하는 함수였다.
- 익숙하지 않아 적응이 필요할 것 같다.
```swift
func swap(record: (int, int)) -> (int, int) { ... }
```
