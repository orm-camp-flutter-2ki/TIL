---
title: 003 FutureBuilder
author: Kim Donghyeok
created_at: 2024-04-24
updated_at: 2024-04-24
tags:
  - 생존코딩
  - 오름캠프
  - flutter
---

# Future

> <https://api.flutter.dev/flutter/dart-async/Future-class.html>

Future 는 dart 언어에서 비동기 연산의 결과를 나타낼 때 사용한다.

비동기연산은 파일 입출력, DB 쿼리 등과 같은 프로그램 외부의 응답을 기다려야 할 때, 동기연산과 다르게 그 결과를 즉시 반환하지 못한다.

이러한 연산 작업이 완료될때 까지 기다리는 것 대신에, 언젠가 작업이 완료되어 결과가 반환될 것을 나타는 Future 를 반환한다.

# FutureBuilder

> <https://api.flutter.dev/flutter/widgets/FutureBuilder-class.html>

Future는 flutter 에서 비동기 연산을 한 결과를 나타낼 때 사용한다.

이러한 Future를 UI로 표현할 할수 있는 방법은 다음과 같다.

1. StatefulWidget + setState()  
2. **FutureBuilder**  

```dart
FutureBuilder(
    future: http.get('http://awesome.data'),
    builder : (context, snapshot) {
        return AwesomeData(snapshot.data);
    }
)
```

- FutureBuilder 는 Future 함수의 결과를 Widget 으로 변환하는 위젯이다.

- snapshot 에 데이터와 에러정보 등이 들어있다.

```dart
FutureBuilder(
    future: http.get('http://awesome.data'),
    builder : (context, snapshot) {
        if(snapshot.connectionState == ConnectionState.done) {
            return AwesomeData(snapshot.data);
        } else {
            return CircularProgressIndicator();
        }
    }
)
```

```dart
ConnectionState.none
ConnectionState.wating
ConnectionState.active
ConnectionState.done
```

- snapshot 객체에서 연결상태를 알 수 있다.

```dart
FutureBuilder(
    future: http.get('http://awesome.data'),
    builder : (context, snapshot) {
        if (snapshot.connectionState == ConnectionState.done) {
            if (snapshot.hasError) {
                return SomethingWrong();    
            }
            return AwesomeData(snapshot.data);
        } else {
            return CircularProgressIndicator();
        }
    }
)
```

- `snapshot.hasError` : snapshot 에서 에러 체킹이 가능하다.
