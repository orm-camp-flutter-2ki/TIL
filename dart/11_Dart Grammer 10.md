## 정규식 ( Regular Expression )

### 정규식 패턴

정규식은 문자열 내에서 특정 패턴을 표현하는데 사용(ex. 이메일 주소, 전화번호, URL 등과 같이 일정한 패턴을 갖는 문자열을 찾거나 추출/ 대체할 때 유용)

- **`.`**: 어떤 한 문자와 일치
- **`[]`**: 문자 집합을
- **`^`**: 문자열 또는 문자 집합의 시작. **`^a`**는 문자열의 시작이 'a'로 시작하는지 확인
- **`$`**: 문자열의 끝 **`a$`**는 문자열이 'a'로 끝나는지 확인합니다.
- **``**, **`+`**, **`?`**: 각각 0회 이상, 1회 이상, 0 또는 1회
- **`{n}`**, **`{n,}`**, **`{n,m}`**: n회, n회 이상, n회부터 m회까지의 반복
- **`\`**: 이스케이프 문자로 사용됩니다. 특수 문자를 일반 문자로 처리하려면 **`\`**를 사용

## 예외 처리

### 예외 처리의 흐름
![10-1](https://github.com/jungeun272/TIL/assets/131224099/381663f7-52f0-405c-bb38-c899422fbd24)

```dart
try {
//에러가 날 것 같은 코드 작성
} catch (e) {
// e: 에러의 정보를 담고 있는 객체
}
```

1. try-catch 문: try 블록 내에 예외가 발생할 수 있는 코드를 작성, catch 블록은 예외의 타입을 지정하여 특정 예외에 대한 처리
    
    ```dart
    dartCopy code
    try {
      // 예외가 발생할 수 있는 코드
    } catch (e) {
      // 예외 처리
      print('예외 발생: $e');
    }
    ```
    
2. catch 절과 예외 타입: catch 절은 예외 타입을 지정하여 특정 타입의 예외에 대해서만 처리함
    
    ```dart
    dartCopy code
    try {
      // 예외가 발생할 수 있는 코드
    } on ExceptionType catch (e) {
      // 특정 예외 타입에 대한 처리
      print('특정 예외 발생: $e');
    } catch (e) {
      // 기타 모든 예외에 대한 처리
      print('기타 예외 발생: $e');
    }
    ```
    
3. **finally 절**: finally 절은 예외 발생 여부에 상관없이 항상 실행되는 코드 주로 리소스를 해제하거나 정리하는 작업에 사용
    
    ```dart
    dartCopy code
    try {
      // 예외가 발생할 수 있는 코드
    } catch (e) {
      // 예외 처리
    } finally {
      // 항상 실행되는 코드
    }
    ```
    
4. **throw 문**: 개발자가 직접 예외를 발생시킬 때 사용. throw 문을 사용하여 사용자 정의 예외를 만들거나, 내장된 예외를 다시 발생시킬 수 있음
    
    ```dart
    dartCopy code
    void depositMoney(int amount) {
      if (amount <= 0) {
        throw Exception('양수만 예금할 수 있습니다.');
      }
      // 예금 처리
    }
    ```
    
    ## 파일 조작
    ![10-2](https://github.com/jungeun272/TIL/assets/131224099/fdfc50f1-ccc0-499b-845d-84868aed6465)
    
    ## 여러가지 데이터 형식
    
    CSV (comma-separated values)
    
    XML (Extensible Markup Language)
    
    JSON (JavaScript Object Notation)
    
    - Json이 컴퓨터나 인간이나 더 읽기 쉽다
    - map 형태
    
    ### 직렬화 역직렬화
    
    - 통신하기 쉬운 포맷으로 변환하는 과정
    - 다른 사람이 쓸 수 있도록 하는 것이 의의를 둠
    - 클래스 내부에 다른 클래스를 포함하면 모두 직렬화를 해야한다.
