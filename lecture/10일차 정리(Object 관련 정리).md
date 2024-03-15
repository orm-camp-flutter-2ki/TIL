Object 클래스의 기본 기능 (참고로 상속 구조를 보려고 하려면 컨트롤 + h)

1. 모든 클래스는 Object 클래스의 메서드와 프로퍼티를 가지고 있다
2. Object 타입 변수에는 모든 인스턴스를 대입할 수 있다

<Object 클래스의 대표 메서드 및 프로퍼티>

- toString() : 문자열 표현을 얻음
- operator == : 비교
- hashCode : 해시값을 얻음

모든 객체는 Object객체를 상속받는다. 개발자가 명시적으로 Object를  상속받는다고 명시하지 않아도 묵시적으로 상속됨

dynamic 은 타입체크를 하지 않아서  nullable타입과 non-nullable타입 모두 다 들어갈 수 있고 .(점)찍고 아무 매소드를 호출하는 코드를 짜도 컴파일 타임에서 오류를 출력하지 않는다. 
하지만 Object 은 non-nullable한 타입들의 최상위 타입이기도 하고 Object 안에 있는 메서드만을 사용할 수 있게 하고 잘못 적을 경우 컴파일 타임에 오류가 난다.

- toString() : 객체를 표현(속성등)하는 문자열 표현을 얻음 재정의(override) 필요시 해야함

- operator == : 비교

객체가 같은 객체인지 비교 시 기본적으로 주소값부터 비교하는데 주소값 비교가 아니라 다른 방법으로 규칙을 정의하기 위해서 bool operator == 메소드를 을 재정의(override)해야 한다. 

이때 hashCode도 같이 재정의 해야한다. 이유는 set과 map은 hashCode 코드를 기반으로 동등성 비교하고 List는 ==으로 동등성을 비교한다.

set이 List보다 빠른이 유는 hashCode 값가지고 찾기 때문이다. 즉 hashCode로 set은 동작한다.

Map도 해시코드 기반이다. 

hashCode 

객체를 내용을 정해진길이의 숫자로 표현하는것 의미

해시코드는 일정하지 않은 길이의 내용을 정해진길이의 숫자로 표현한다.

dart에서 hashCode 함수를 통해서 객체의 해시코드값이 정해지게 되고 이는 

set과 map에서 동일성 비교에 사용된다. 앞서 == 재정의 시에 hashCode를 

재정의 해야하는 이유를 좀 더 자세히 설명하자면 ==은 list, set과 map는

hashCode함수를 통해서 동일성비교하게 되는데 ==만 재정의 한다면 set과 

map에서 동시성비교할때 List와 다른 결과를 불러올 수 있다. 그래서 동일하게 맞추어 주기 위해서 

같이 재정의를 해야하는 것이다.

참고로 동일성 재정의하려고 ==과  hashCode 를 재정의시 맴버변수에 

기본자료형 객체가 아닌 일반자료형의 객체가 있는 경우 해당 멤버변수의 클래스에서 

  ==과  hashCode 를 재정의가 필요하다.

List

List.sort() 메서드는 컬렉션 내부를 정렬해 줌

[https://api.flutter.dev/flutter/dart-core/List/sort.html](https://api.flutter.dev/flutter/dart-core/List/sort.html)

```dart
final names =['Seth','katy','Lar'];
name.sort((a,b) => a.compareTo(b));//오름차순으로 정렬 a.compareTo(b) * -1 하면 내림차순정렬
print(name.reversed);//내림차순 출력 reversed 는 프러퍼티로 단지 표현만 
                     //내림차순 해주고 실제정렬 안됨
print(name);//reversed는 실제 내부요소 정렬 안해주어서 기존정렬된 것처럼 오름차순 출력                    
```

하지만 sort() 메서드를 사용하기 위해서는

다음과 같은 제약이 따름

정렬 대상이 **Comparable 인터페이스**를 구현하거나

sort 함수가 직접 정렬 대상의 정렬 규칙을 **Comparator 함수**로 구현해야 함

![Untitled](https://github.com/happysong3914/TIL/assets/130008915/4f9fa3df-4d1c-46b0-a91d-c3840d0f3197)


실제로 compareTo는 함수는 하나이다.  static 붙어 있는 것은 별도의 공간에 있는 것으로 생각하며  클래스명.compareTo()으로 사용하여야 해서이다 

implements Comparable<T> 해서 추가적으로 구현해야 하는 메서드는 static 안 붙은

추상메서드 int  compareTo(T other); 하나이다.

deep copy

Dart에서는 깊은 복사를 위한 별도의 기능을 지원하지 않습니다.

직접 작성해서 사용해야 함

```dart
Person copyWith({
	String? name,
	int? hp
}) {
	 return Person(
		 name: name ?? this.name,
		 age: age ?? this.age,
	 );
}
```
