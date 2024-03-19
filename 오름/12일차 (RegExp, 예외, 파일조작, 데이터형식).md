### 과제리뷰)

- 제네릭: class StrongBox<E> 여기서 E는 열쇠가 아닌 물건을 말함. 사실 ITEM이라고 써도 되나, 이왕이면 대문자로 한글자 쓰는 것 지향하기

- enum+switch : 키 값을 정하기 위한 것.

- 테스트코드 정리: (종호님 자료 제공: [가독성 좋은 테스트 코드를 작성하는 방법 | 요즘IT (wishket.com)](https://yozm.wishket.com/magazine/detail/2435/))

- substring(0, 2) ⇒ 0번에서 2번까지

## 1. 정규표현식(RegExp)

1. **문자열 검색 및 추출:** 정규 표현식을 사용하면 문자열 내에서 특정 패턴을 검색하고 추출할 수 있다. 예를 들어, 이메일 주소, 전화 번호, URL 등과 같은 특정 패턴을 찾아내고 추출할 수 있다.
2. **문자열 대체:** 문자열 내에서 특정 패턴을 찾아서 다른 문자열로 대체할 수 있다. 이를 통해 문자열 내의 특정 단어나 구문을 교체하거나 수정할 수 있다.
3. **문자열 유효성 검사:** 입력된 문자열이 특정 규칙을 준수하는지 확인할 수 있다. 예를 들어, 사용자가 입력한 비밀번호가 특정 요구 사항을 충족하는지 여부를 확인하는 데 사용할 수 있다.
4. **텍스트 처리 및 분석:** 텍스트 데이터를 처리하고 분석할 때 정규 표현식은 매우 유용함. 텍스트 데이터에서 원하는 정보를 추출하거나 특정 패턴을 식별하는 데 사용할 수 있다.
5. **파일 이름 및 경로 처리:** 파일 이름이나 경로에서 특정 요소를 추출하거나 변형하는 데 사용될 수 있다.

ex) 첫 글자가 영어로 시작하는 A~Z, 0~9 사이의 8자리 문자

```dart
bool isValiaPlayerNmae(String name) {
 return RegExp(r' [A-Z][A-Z0-9]{7}').hasMatch(name);
 }
```

```dart
  bool isVowel(int i) {
    return 'aeiou'.contains(word.substring(i, i + 1).toLowerCase());
  }
  
  
  이것을 아래처럼 할수도 있음.
  
    bool isVowel(int i) {
    return RegExp(r'[aeiou]').hashMatch(word.substring(i, i+1));
  }
  
```

---

## 2. 예외

프로그램을 설계할 때실행시에 예외 상황이 발생 할 가능성이 있는 것을 예측하여, 사전에 예외 처리가 되도록 할 필요가 있음. 이럴 때 적절한 조치가 없으면 프로그램은 에러가 나며 죽어 버림.

1. 문법 에러 (syntax error)  = 컴파일 에러
2. 실행 시 에러 (runtime error)
3. 논리 에러 (logic error) = 휴먼 에러

- 예외 처리(try

```dart
try {
  //에러가 날 것 같은 코드 작성
} catch (e) {
  //e 에러의 정보를 담고 있는 객체
}
```

try-catch 문으로 Exception 계열 예외를 처리

```dart
void main(List<String> arguments){
try {
 someError();
 }catch (e) {
  print(e);
  }
  }
  
  void someError(){
 // 뭔가를 하는 코드
 throw FormatException('에러가 발생했습니다');
 
 
 
 안터지고 print(e);가 실행이 됨
```

## 2. 파일조작

파일을 복사하는 함수를 만들려면 파일을 읽고 쓰는 방법을 이해해야 함.

**1) 파일 쓰기: writeAsStringSync**

```dart
//파일 열기
final myFile = File('save.txt');

// 내용 쓰기
myFile.writeAsStringSync('Hello, world!');

```

**2) 파일 읽기: readAsStringSync**

```dart
final file = File('save.txt');

final text = file.readAsStringSync();
print(text);
```

- **\n = 엔터**
- **\t\ = 탭**

따옴표 3개 치면 그 안에서 따옴표, tab 등 다 해도 괜찮음. (엔터는 **\n로..)**

---

```dart
final myFile = File('save.txt');   // 열겠다고 선언

// 내용 쓰기
myFile.writeAsStringSync('Hello, world!'); //append는 추가로 붙이는 것
file.writeAsStringSync('Hello World');
file.writeAsStringSync('\nHello World');  //excape시퀀스

//파일 복사하는 것
void copy(String source, String target){

}
```

---

## 3. 여러가지 데이터 형식

### **1) CSV (comma-separated values)**:

- 데이터를 콤마로 나눈 형식

```dart
String str = '홍길동, 한석봉, 신사임당';

```

### 2) 프로퍼티 형식의 파일 읽기

- 프로퍼티 클래스를 사용하여 키(key)와 값(value)의 쌍으로 읽고 쓰기 가능
- =으로 잘라서 첫번째꺼는 key value, 두번째 것이 이름이다.

### 3) XML 형식(**(Extensible Markup Language)**

- <>태그를 활용한 기술 방식. 포함관계를 기술할 수 있음
- <to> 여는 태그, </to> 닫는 태그
- DOM Parser, SAX Parser 등을 통해 파서를 제작할 필요가 있음

### 4) JSON 형식 **(JavaScript Object Notation)**

- 네트워크 통신에서 가장 많이 사용되고 있음
- XML에 비해 적은 용량
- []로 리스트, { } 로 객체를 표현
- 키(key): 값(value) 형태
- Dart의 MAP<String, Dynamic>과 똑같이 생김.

### **5) 직렬화(encoding)**

컴퓨터에서 직렬화(serialization)란 데이터 구조나 객체를 저장하거나 전송 가능한 형태로 변환하는 프로세스를 의미.

직렬화는 객체를 파일에 저장하거나 네트워크를 통해 다른 시스템으로 전송할 때 사용.

직렬화를 거치면 객체의 상태나 데이터 구조가 바이트 스트림으로 변환되어, 이를 다시 역직렬화(deserialization)하여 객체로 복원할 수 있다.

- 데이터 구조나 객체 상태를 저장하고 나중에 재구성할 수 있는 포맷으로 변환하는 과정
- 객체를 파일의 형태 등으로 저장하거나, 통신하기 쉬운 포맷으로 변환하는 과정을 의미
- 클래스 내부의 필드에 다른 클래스가 있다면 모두 직렬화 처리를 해 줘야 함

직렬화 : 클래스 -> Json

역직렬화 : Json -> 클래스

```dart
*** <역직렬화> = fromJson(): json(실제로는 Map)으로부터 객체를 생성하는 생성자**
 User.fromJson(Map<String, dynamic> json)
  : name = json['name'],
    email = json['email'];
    
   
    
*** <직렬화> = toJson() : 객체를 Json 형태로 표현하는 메서드**
Map<String, dynamic> toJson() => { 
 'name': name,
 'email: email,
 };
 }

```

- jsonDecode() 함수: 문자열로 된 코드를 json으로 바꿔주는 함수.

- jsonEncode()함수: Map 을 Json 형태의 String 으로 변환
