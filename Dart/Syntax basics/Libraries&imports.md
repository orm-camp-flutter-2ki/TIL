# Libraries & imports
[공식문서](https://dart.dev/language/libraries)

- `import`와 `library`지시문은 모듈화와 공유 가능한 코드 베이스를 만드는 것을 도와준다. 
- 라이브러리는 API뿐만 아니라, privacy 유닛도 제공한다.  
    => Dart의 프라이빗(`_`)은 같은 라이브러리 내부에서만 접근 가능하다.
- Dart의 파일은 기본적으로 하나의 라이브러러이다.
- 라이브러리는 packages를 통해서도 구분이 가능하다.

<br>

## 라이브러리 사용
- `import [경로];`를 통해 라이브러리를 사용(import)할 수 있다.
- Dart 내장 라이브러리는 경로가 `dart:`로 시작한다.
- 다른 라이브러리는 해당 라이브러리가 있는 시스템 경로나 `package:` scheme을 사용한다.  
    => `package:` scheme는 pub tool과 같은 패키지 매니저로부터 제공 받은 라이브러리를 지정한다.

<br>

### 라이브러리 prefix
`as`를 통해 라이브러리의 prefix를 지정할 수 있다.  
=> 이를 통해 서로 다른 라이브러리에 속한 같은 이름의 클래스, 변수, 메서드를 구분할 수 있다.   
```dart
import 'package:lib1/lib1.dart';
import 'package:lib2/lib2.dart' as lib2;

// Uses Element from lib1.
Element element1 = Element();

// Uses Element from lib2.
lib2.Element element2 = lib2.Element();
```

<br>

### 라이브러리의 일부만 import
- `show`를 통해 라이브러리의 일부만 import  
    => `import 'package:lib1/lib1.dart' show foo;`
- `hide`를 통해 일부만 제외하고 모두 import  
    => `import 'package:lib1/lib1.dart' hide foo;`

<br>

## 라이브러리 지연 로딩
**dart compile js에서만 지원**  
라이브러리 지연 로딩은 웹앱이 라이브러리가 필요할 때 가져오는 것으로 다음의 상황에서 사용된다.  
- 웹앱의 초기 실행에 필요한 시간 감수
- A/B 테스트  
    ex) 대체 알고리즘 테스트
- 거의 사용 되지 않는 기능 로드

<br>
 
 ### 라이브러리 지연 로드 사용법
 1. 먼저 `deferred as`를 통해 라이브러리를 import한다.
    => `import 'package:greetings/hello.dart' deferred as hello;`
2. 라이브러리가 필요할 때 라이브러리 식별자를 통해 `loadLibrary()`를 실행한다.  
    => `loadLibrary()`를 여러번 호출해도 된다. 단, 실제 로드는 한번만 됨.
    ```dart
    Future<void> greet() async { 
    // await: 라이브러리 로드될 때까지 잠시 실행을 중지 시킴
    await hello.loadLibrary();
    hello.printGreeting();
    }
    ```

<br>

### 라이브러리 지연 로드 주의 사항
- 지연 로딩되는 라이브러리의 상수는 importing하는 파일에서는 상수가 아니다.  
    => 로드되기 전까지 상수는 존재하지 않음
- 지연 로딩되는 라이브러리의 타입을 importing하는 파일에서 사용할 수 없다.
- Dart는 암시적으로 `deferred as`로 지정한 네임스페이스에 `loadLibrary`를 삽입한다.
    => `loadLibrary()` 함수는 `Future`를 반환