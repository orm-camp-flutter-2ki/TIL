# 모델 클래스, 레포리티지 개념

## Model class 의 책임과 역할

- 모델 객체 클래스의 속성에 대한 데이터를 조회할 수 있는 클래스
- 별도의 기능을 가지지 않는 순수한 클래스 (map, copyWith …은 기능이 아님(데이터 클래스 6종 세트 포함))
- 데이터 소스를 앱에 필요한 형태로 변환하여 앱 개발을 편리하게 해 주는 역할
- 내용/ 생성자/ final
- 뷰에 보여질 데이터를 담는 객체

## 모델링 방법

- DDD (Domain Driven Design)
    - 유사한 업무의 집합
    - 특정 상황(주문, 결재, 로그인)이나 특정 객체(유저, 손님)가 중심이 될 수 있음
- ORM (Object-relational mapping)
    - 데이터 소스가 DB 인 경우 DB 와 모델간 상호 변환을 도와주는 기법
    - ORM은 DB 를 활용할 경우에 따로 살펴봐도 됨
    - 지금은 이런게 있네 하고 넘어가자

## Repository

- 데이터 소스와 상호 작용하여 데이터를 추가, 조회, 수정, 삭제(CRUD)하는 역할을 담당
- **데이터 캡슐화**
- **데이터 추상화**
- 데이터 접근 제어
- 예외 처리

**불변**
```dart
class User {
  final String name;
  final String email;
  
  const User(this.name, this.email); // const 키워드 사용
}
```
