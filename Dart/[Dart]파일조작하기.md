> **파일 조작의 기본 순서**
1. 파일을 연다
2. 파일을 읽거나 쓴다
3. 파일을 닫는다
```dart
import 'dart:io'; // import html붙은거 임포드 하면 안됨
//파일열기
final myFile = File('save.txt')';
//열고 쓰거나 읽고 닫는다 다만 쓸때는 기존내용 삭제되고 다시 써짐
myFile.writeAsStringSync('Hello, world!');
//mode:Filemode.append 기존내용 붙여넣기 위해서 추가 설정 넣어놈
myFile.writeAsStringSync('Hello, world!', mode:Filemode.append);
//파일읽기
final test = myFile.readAsStringSync();
```
_tip)<br>다양하게 써야 되면 ```백틱3개``` ,```  사용해서 모두 작성가능 <br>하지만 엔터 안됌->  /n사용해서 엔터 작성 _


> **_예시) 파일복사하기_**
```dart
import 'dart:io';
void Copy(String source, String target) {
  try {
    // 파일 경로 저장
    final sourceFile = File(source);
    // 복사할 파일
    final targetFile = File(target);
    // 복사할 파일 경로에 있는 파일 읽어서 내용값에 저장
    final contents = sourceFile.readAsStringSync();
    // 복사할 파일에 파일 내용 적기
    targetFile.writeAsStringSync(contents);
    print('파일복사완료');
  } catch (e) {
    print('복사실패 ${e}');
  }
}
```
_**test code)**_
```dart
import 'dart:io';
import 'package:learn_dart_together/240319/copy.dart';
import 'package:test/test.dart';
void main() {
  test('copy Test', () {
    //파일 생성
    File book = File('book.txt');
    // 내용 추가
    book.writeAsStringSync('내용내용');
    // 파일 경로 복사
    Copy('book.txt', 'bookCopy.txt');
    // 파일에 복사한 파일 경로 저장
    final testCopyFile = File('bookCopy.txt');
    // 파일에 복사한 파일 내용 읽어서 내용  저장
    final contentCopy = testCopyFile.readAsStringSync();
    // 내용 확인
    expect(contentCopy, equals('내용내용'));
  });
}
```
