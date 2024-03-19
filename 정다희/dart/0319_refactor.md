# 테스트코드 더 세밀하게 짜는법

```dart

void main() {
  group('test하고싶은 큰주제', () {
    setUp(() {
      // 테스트 진행전 셋팅할 값
    };
        tearDown(()
    {
      // 테스트가 끝난 후 진행할 코드
    };))
  })
}

//given
//when
//then으로 나눠서 작성해보기

// 모든 경우에 대해서 테스트를 작성해야 한다.
//isVowel 코드의 경우 aeiouAEIOU 에 대해서 모두 검사해아함.
//consonant 함수도 aeiou를 제외한 모든 문자에 대해서 검사해야함.
// 예외 케이스를 늘 생각해야 한다. 입력값이 문자가 아니면? 입력값이 양수가 아니면?
```

# switch를 표현식으로 쓸 수 있음

```dart

final keyCount = switch(_keyType){
  KeyType.padlock => 1024,
  KeyType.button => 10000,
  KeyType.dial => 30000,
};
```

# 예외

## 실행시 예외 상황이 발생할 가능성을 예측하여 사전에 예외처리 할 필요!

- 예외처리 안하면 프로그램 죽음

## 에러종류

- 문법에러
- 실행시 에러
- 논리 에러(젤 잡기 힘듦!!!) -> 실행하면 예상 외의 값이 나옴.

## 예외적인 상황들

- 메모리 부족
- 파일 not found
- 네트워크 통신 불가 등

## 예외처리의 흐름

```dart
void main() {
  try {
  예외 날것같은 코드 }
  catch (e){print(e)} //터지지않고 catch 안에 코드가 실행됨
}

```

## 강제로 에러를 발생시킬 수도 있음.

throw FormException('에러 발생'!); // 터짐

## rethrow

현재 처리중인 예외를 다시 발생시키는데 사용됨
예외 처리를 위해 try-catch 블록을 사용할떄 catch 블록 안에서 특정 조건을 처리한 후에
원래 발생한 예외를 상위 코드로 다시 전파해서 추가적인 처리를 하기 위함.
한줄요약 = 폭탄돌리기

## 특정 예외를 잡을 수도 있음

```dart
try {
someError();

} on FormatException {
print('FormatException 이 발생했습니다')
} finally {
print('무조건 실행되는 코드')
}
```

# 파일 읽기 쓰기

```dart

final file = File('save.txt');
file.writeAsStringSync
("hello world
"
);
// 쓰거나 읽거나 닫을 수 있음.
```

# 데이터 형식

## CSV(comma seperated values)

데이터를 콤마로 나눈 형식
엑셀에서 주로 사용됨

## XML 형식 (extensible markup language)

ex) HTML
<> 태그를 활용한 기술 방식
포함관계를 기술할 수 있음

## JSON형식

네트워크 통신에서 가장 많이 사용됨
XML에 비해 적은 용량
[]로 리스트, {}로 객체를 표현
키:값의 형태
Dart의 Map 과 똑같이 생김

## 직렬화란? (serialization)

데이터 구조나 객체 상태를 저장하고 나중에 재구성할 수 있는 포맷으로 변환하는 과정
통신하기 쉬운 포맷으로 변환하는 과정
클래스 내부에 다른 클래스가 있다면, 모두 직렬화 처리 해야함.

## dart의 직렬화란 ?

- 직렬화 : 클래스 ->Json
    - toJSON() 메서드 : 객체를 json 형태로 표현하는 메서드
- 역직렬화: Json -> 클래스
    - fromJson() 메서드 : json 으로부터 객체(인스턴스)를 생성 하는 생성자

## 서버에서 응답값은 string 화 된 json으로 들어옴

사용하려면 jsonDecode 사용하면 map 자료형으로 받을 수 있음.
반대로 Map을 Json 형태의 String으로 변환하려면 jsonEncode


