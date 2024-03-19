## 1. 에러(Exception)
### 에러의 종류
* 문법 에러(syntax error)
* 실행 시 에러(runtime error)
* 논리 에러(logic error)

<img width="788" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/cb6389e4-f6cb-45d4-bc0e-3a704c00e791">

### 예외적인 상황들
* 메모리 부족
* 파일을 찾을 수 없음
* 네트워크 통신 불가 등

### 에러 처리
* try-catch문으로 특정 예외를 처리 <p>
<img width="400" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/7e6e13f7-5467-4bce-ba8d-34c487bb3da7"> <p>
* try-catch문의 finally 블록으로 나중에 꼭 해야하는 처리를 할 수 있다.
* throw문을 사용하면 임의로 예외를 발생시킬 수 있다.
  * implemeter에 다양한 exception과 error의 종류가 있기 때문에 에러 타입을 나타내는 implemeter 사용하는 것 권장.

```dart
// throw 예시
throw FormatException('Expected at least 1 section');
```

<br></br>

## 2. 파일(File)
### 파일 경로 생성(확인)
```dart
final myFile = File('save.txt')
```

### 내용 쓰기
```dart
myFile.writeAsStringSync('Hello, world!');
```

### 내용 읽기
```dart
final text = myFile.readAsStringSync();
print(text);
```

<br></br>

## 3. 여러가지 데이터 형식(Data type)
### 데이터 형식
* CSV
  * 데이터를 콤마(,)로 나눈 형식
```dart
String str = '홍길동, 철수, 신사임당';
```

* 프로퍼티 형식
  * Properites 클래스를 이용하여 키(key)와 값(value)의 쌍으로 읽고 쓰기가 가능
```dart
hereName=홍길동
hereHp=100
```

* XML 형식
  * <> 태그를 활용한 기술 방식
  * 포함 관계를 기술할 수 있음
  * DOM Parser, SAX Parser 등을 통해 파서를 제작해야 함
<img width="567" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/9f423f66-8a45-4c91-83ed-e8e2eb1b8e47">

* JSON 형식
  * 네트워크 통신에서 가장 많이 사용되고 있음
  * XML에 비해 적은 용량
  * [] 로 리스트, {} 로 객체를 표현
  * 키(key) : 값(value) 형태
  * Dart의 Map<String, dynamic>과 똑같이 생겼음
<img width="585" alt="스크린샷 2024-03-19 오후 7 20 38" src="https://github.com/NalaJang/TIL/assets/73895803/5363f2cf-7471-42f3-af51-20fe96470dbf">

### Dart의 직렬화(Serialization)
### 직렬화
* 데이터 구조나 객체 상태를 저장하고, 나중에 재구성할 수 있는 포맷으로 변환하는 과정
* 객체를 파일의 형태 등으로 저장하거나, 통신하기 쉬운 포맷으로 변환하는 과정
* 클래스 내부의 필드에 다른 클래스가 있다면 모두 직렬화 처리를 해 줘야 함
* 클래스 -> Json
* toJson() 메서드

### 역직렬화
* Json -> 클래스
* fromJson() 생성자
```dart
// fromJson() : json (실제로는 Map) 으로부터 객체를 생성하는 생성자
Employee.fromJson(Map<String, dynamic> json)
  : name = json['name'],
    age = json['age'];

// toJson() : 객체를 Json 형태로 표현하는 메서드
Map<String, dynamic> toJson() => {
    'name' : name,
    'age' : age,
  };
```

### String 형태의 Json을 Map으로 변환
* jsonDecode() 함수 사용
```dart
String jsonString = '{"name": "John Smith", "email": "john@example.com"}';
Map<String, dynamic> json = jsonDecode(jsonString);
```

### Map을 Json 형태의 String으로 변환
* jsonEncode() 함수 사용
```dart
Map<String, dynamic> json = {"name": "John Smith", "email": "john@example.com"};
String jsonString = jsonEncode(json);
```
