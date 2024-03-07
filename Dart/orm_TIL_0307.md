240307 (Thu)

플러터 과정 4일차
=
NULL safety
--
NULL이란 값이 존재하지 않는 변수를 의미한다. 
Dart에서 null을 사용하기 위해서 장치를 하나 마련했는데 그것이 Dart가 NULL safety 언어라 불리는 까닭이다.
NULL값을 Dart에 사용하기 위해서는 int, double 등의 타입 함수 뒤에 ?를 사용해서 쓸 수 있다.

ex) int? a = null; , int? b;
위와 같이 사용할 수 있다.

int 와 int?는 다른 타입의 변수이다.

?? : 앞에 객체가 NULL인 경우에 사용한다. 
ex) nullAbleValue ?? 0

! : nullable인 값을 null이 아님을 보증하는 코드이다. 하지만 잘 쓰지 않는데 만약 변수가 NULL인 경우 런타임 오류를 발생시키기 때문이다.


용어 정리
-
object 오브젝트 : 현실 세계의 몯느 객체
class 클래스 : 오브젝트를 가상 서계 용으로 구체화 한 것
instance 인스턴스 : 클래스를 활용해 메모리 상에 만들어 낸 것

class에서

string, int, double을 사용 할때

변수 이름만 사용해도 된다.

단, class 명에 따른 코드를 짜준다.

ex)
class Hero{

  String name;

  int hp;

  Hero(this.name, this.hp);
}

클레스 안에 변수들을 필드, 전역변수, 멤버변수라고 한다.


클래스 네이밍 규칙

| 클래스 명 | 명사 | 단어의 맨 처음은 대문자 (pascal) | Hero, MonsterInfo |
|||||
| 필드 명 | 명사 | 최초 이외의 단어의 맨처음 대명사는 대문자 (camel) | intValue |
| 메소드 명 동사 | 동사 | 최초 이외의 단어의 맨처음 대명사는 대문자 (camel) |  |
