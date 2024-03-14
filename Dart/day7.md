# 추상클래스와 인터페이스

- abstract
1. 추상클래스는 인스턴스화 불가능
2. (puml 작성)
- 기울어져 있는 테스트 → 추상 클래스
- 작성방법 {abstract} void methods()


- interface
1. 모든 메소드는 추상 메소드 여야 한다
2. 필드를 가지지 않는다
3. 기능이 구현된게 아무것도 없음 다른클래스에서 구현해서 쓴다.의 의미로 사용
4. 모든 메서드를 다 구현하지 않아도 됨
5. 복수의 인터페이스를 부모로 두는 다중상속 효과가 가능

```
abstract class korean extends Person implements Human {}  // korean 은 Person을 상속받으며 Human을 구현함
```
