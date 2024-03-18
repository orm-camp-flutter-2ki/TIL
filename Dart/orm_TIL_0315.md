240315

플러터 과정 10일차

# 오브젝트 Object(객체)

```dart
int i = 10;
double d = 10.5;
String s = i.toString();

num number = 10;
number = 10.5
Person person = Person();

//NO 근본이 없다.
dynamic dynamic2 = person();
dynamic2 = 10;
dynamic2 = 10.5;
dynamic2 = 'tttt';
// 다이나믹은 없는것도 있는것처럼 사용되기 때문에 사용해서는 안된다.
// 다이나미은 null값도 사용이 되서 명확하지 않다.

//Ok 근본이 있다.
object object = person;
object = 10;
object - 10.5;
object - 'tttt';

if( object is String){
	String text = object;
	}
}
// Object 타입은 non_nullable한 타입의 최상위 타입이기 때문에 가능
```

toString()

오버라이드하여 원하는 결과를 얻도록 수정할 수 있음

우클릭 후 제네레이트 버튼 누르면 

toString을 사용할 때 어느 메소드를 사용하면

재정의가 필요하다.

list에서는 final이나 const 를 포함해서 넣는다면 어떻게 될까?

답은 list에서는 중복과 순서를 중요시 하기때문에 final이나 const 상관없이 들어간다.

== 연산자를 오버라이드 하지 않는 객체의 상위급

set이 검색기능이 빠른 이유는 hashcode 기반으로 검색하기 때문이다.

String int는 이미 동등성 비교 규칙이 적용되어있다.

순서 정렬 sort

[a.compare](http://a.compare)To

sort 에서 룰을 바꾸는 것(오름차순에서 내림차순으로 구하는)은 * -1 해서 구한다.

sort 기능의 반대되는 코드도 있다.

a.**reversed**

sort의 제약이 있다.

정렬 대상이 comparable

comparable은 메소드가 1개

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/86296f50-858e-40b3-b09a-5faedc04c2f9/94bde85c-65dc-48d9-b607-cf656f7ce01c/Untitled.png)

comparble 정의 하는 방법

*static 함수는 다른 메모리를 사용하는 것 comparable 내의 메소드가 아니다.

typedef 라고 클래스 내부에 임시로 함수를 주는것

```dart
  @override
  bool operator == (Book other) =>
      identical(this, other) ||
  other is Book &&
    title == other.title &&
  publishDate == other.publishDate;
  }

  @override

```

객체지향 프로그램

블럭, 조립 로봇처럼 코딩

왜?

+비용

새로운 코드 생성, 추가, 삭제 ,수정

설계

협력과 메세지

역할/책임 = (→다형성)
