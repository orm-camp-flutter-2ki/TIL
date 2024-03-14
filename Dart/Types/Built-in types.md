# Built-in types
[공식문서](https://dart.dev/language/built-in-types#runes-and-grapheme-clusters) 

따끈따끈한 언어답게, Dart의 모든 것은 객체이다.  

Dart는 개발자들의 편의를 위해 아래의 타입에 대해 생성자가 아닌 다른 방식으로 객체를 생성할 수 있도록 지원한다.
- Numbers (int, double)
- Strings (String)
- Booleans (bool)
- Records ((value1, value2))
- Lists (List, also known as arrays)
- Sets (Set)
- Maps (Map)
- Runes (Runes; often replaced by the characters API)
- Symbols (Symbol)
- The value null (Null)

<br>

아래의 타입들은 Dart에서 특별한 역할을 하는 타입들이다.  
- Object: null을 제외한 Dart의 모든 클래스의 부모(super)클래스  
- Enum: 모든 enum의 부모 클래스  
- Future, Stream: 비동기 지원에 사용  
- Iterable: for-in 반복문과 동기 제네리이터에 사용  
- Never: 해당 표현식이 절대 성공적으로 끝날 수 없음을 나타냄    
    => 항상 예외를 던지는 함수에 주로 사용  
- dynamic: static 타입 검사를 disable    
    => dynamic 대신 `Object`, `Object?`를 사용할 것  
- void: 해당 값이 절대 사용되지 않음을 명시  
