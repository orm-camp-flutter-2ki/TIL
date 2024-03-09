# Nullable을 안전하게 다루는 방법
## 1.강제언래핑을 통해 널러블 해제
```dart
final int code = 100;
final String? error = null;

String toString() {
  if (code == 200) return 'OK';
  return 'ERROR $code ${error!.toUpperCase()}';
}
```
```
Unhandled exception:
Null check operator used on a null value
#0      dd.toString (package:learn_dart_together/240308/cleric.dart:39:32)
#1      main (package:learn_dart_together/240308/cleric.dart:51:6)
#2      _delayEntrypointInvocation.<anonymous closure> (dart:isolate-patch/isolate_patch.dart:297:19)
#3      _RawReceivePort._handleMessage (dart:isolate-patch/isolate_patch.dart:184:12)
```
- 방법은 옵셔널을 처리하는 방법과 동일해보임. `!`를 활용하여 해제하는 듯 함.
- 아래와 같은 코드를 실행했을 때 swift와 동일하게 런타임오류가 발생함.(위험, 사용지양)


## 2. if문으로 null check & 옵셔널체이닝
```dart
  String toString() {
    if (code == 200) return 'OK';
    if (error != null) {
      return 'ERROR $code ${error?.toUpperCase()}';
    }
    return 'someCode';
  }
```
- if문으로 null check하는 방법임.
- if let 구문처럼 옵셔널 타입을 if 코드블럭 내부에서 완전히 언래핑하는 것과는 다른 방법으로 보임.
- if 블럭 내부에서도 옵셔널체이닝으로 이를 언래핑해주어야 사용가능한듯?


## 3. ?? 연산자로 null check
```dart
void operatorTest() {
    print(error ?? 'null이라는거죠');
}
```
- 공식문서를 보면 if null 은 ?? 와 같다고 쓰여있다.
- 근데 쓰면 코드가독성 떨어질듯하다. 찾기도힘들 것 같고..
- 한정된 상황에서만 사용하자

## 4. Type Promotion
```dart 
void printLength(String? text){
    if(text == null) {
        throw Exception("The text is null");
    }
    print("Length of text is ${text.length}");
}
```
- [type Promotion in dart 관련문서](https://dart-tutorial.com/null-safety/type-promotion-in-dart/)
- 여기서 만약 Dart의 코드분석이 nullable변수인데 절대 null값을 가질 수 없는 변수를 발견한다면,
- Dart는 이 nullable변수를 non-nullable로 취급한다.
- 함수 내부에서 nullable을 사용하고있다면 예외사항을 모두 체크해주고 non-nullable로 type promotion해서 리턴하는게 가장 안전해보인다.
- 타입프로모션을 애용하자
