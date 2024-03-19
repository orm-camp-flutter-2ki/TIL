240319 (Tue)

플러터 과정 12일차

switch expressions
-
![스크린샷 2024-03-19 093754](https://github.com/BAUu/TIL/assets/44741680/94520ded-7617-4d76-b918-a3fd6c709cb9)

식처럼 사용하는 것

```dart
int keyCount = 0;
    switch(_keyType){
      case KeyType.padlock:
        keyCount = 1024;
      case KeyType.button:
        keyCount = 10000;
      case KeyType.dial:
        keyCount = 30000;
      case KeyType.finger:
        keyCount = 1000000;
    }
```

이러한 식을 switch expressions을 사용한다면

```dart
final int keyCount| = switch (_keyType) {
KeyType.padlock => 1024,
KeyType.button => 10000,
KeyType.dial => 30000,
KeyType.finger => 1000₺00,
};
```

이렇게 바꿀 수 있다.


# 정규식

RegExp

r → rowdata

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/86296f50-858e-40b3-b09a-5faedc04c2f9/0d7ea8c5-7611-4c1e-9dc9-98dcd2d00ea5/Untitled.png)

5 [] : 어느 한 문자

6 [ - ] : 지정 문

# 예외 (Exception)

예외 상황이 발생 할 가능성이 있는 것을 예측해서 사전에 예외 처리가 되도록 하는것

## 에러의 종류와 대응책

1. 문법에러 (syntax error)
2. 실행 시 에러 (runtime error)
3. 논리 에러

에러 상황 별 처리

![스크린샷 2024-03-19 113941](https://github.com/BAUu/TIL/assets/44741680/50eebac7-2ca3-4dbd-b787-0828ab6103b7)


예외 적인 상황들

- 메모리 부족
- 파일을 찾을 수 없음
- 네트워크 통신 불가 등

예외를 발생

throw  aaa Exception(’에러 발생’);

void main(List<String< arguments){

try{

someError()

}  catch () {

}

}

void someError() {

thro FormatException(’error’);

}

rethrow 문 ← 있는 거만 알아도 된다.

특정 예외를 캐치

on FormatException

에러가 나도 마지막에 실행 되는 코드

→ finally

# 여러가지 데이터 형식

### CSV (comma-separated-values)

데이터를 콤마로 나눈 형식

ex) String str = “홍길동, 한석봉, 신사임당”;

### 프로퍼티 형식

### XML (Extensible markup language)형식

<> 태그를 활용한 기술 방식

포함관계를 기술할 수 있음

파서를 제작할 필요가 있음

### JSON 형식

네트워크 통신에서 가장 많이 사용되고 있음

XML에 비해 적은 용량

[ ]로 리스트 , { }로 객체 표현

키: 값 형태

### 컴퓨터의 직렬화의 의미

데이터 구조나 객체 상태를 저장하고 나중에 재구성할 수 있는 포맷으로 변환하는 과정

객체를 파일의 형태등으로 저장하거나, 통신하기 쉬운 포맷을 변환하는 과정을 의미

**클래스 내부의 필드에 다른 클래스가 있다면 모두 직렬화 처리를 해 줘야함**

인코딩 = 직렬화

디코딩 = 역직렬화

serialization/ encoding

desirialization/ decoding

처리해야할 Json  데이터의 형태는 Map의 형태로 되기 때문에 Dart에서는 Map을 활용하여 처리한다.

Map을 Json 형태의  String형태로 변환

→ Jsonencoding
