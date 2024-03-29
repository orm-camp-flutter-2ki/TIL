240328 (Thu)

플러터 과정 19일차

### 오늘 꼭 기억해야할 메모

데이터의 변환 과정

Data -> API -> DTO -> MAPPER -> MODEL -> REPOSITORY -> TEST

![image](https://github.com/BAUu/TIL/assets/44741680/749d65af-ab59-4a08-a05a-134cc987eb43)

expected의 변환 과정  result를 통해 데이터를 받고 이 데이터는 형태가 List<object>이다 하지만 형태를 List<User>로 바꿔야한다.
그래서 일단 map함수로 형태를 List<UserDto>로 바꾸고 Map<> 형태로 바꾸고 다시 한번 더 toUser를 통해서 User 형태로 바꾼뒤에 List<User>
형태로 바꿔주었다.

DTO & Mapper 
=

오늘 공부에서는 지난번 repository와 함께 사용하는 DTO에 대해서 알아보자

DTO (Data Transfer Object)
-
데이터 소스를 모델 클래스로 변환 하느 과정에서 순수하게 클래스에 담기 위한 중간 전달 객체를 의미한다.

왜 중간에 전달하는 객체를 만드는 이유는 데이터 소스가 항상 완벽하게 모든 데이터를 가지고 있지는 않다.
그래서 잘못된 데이터를 받더라도 안 터지게 하기위한 방어 수단이다.

DTO를 추가시 변경점
-
기존 데이터 클래스에 있는 6종 hashCode, ==, fromJson, toJson, toString, copyWith 중에서 데이터를 받거나 보내는 
코드인 fromJson과 toJson을 DTO 코드에 추가 시키고 기존 데이터 클래스에는 4종 만을 남겨 놓는다.

Mapper
-
맵퍼는 Dto 를 모델 클래스로 변환하는 유틸 메소드이다.
확장함수 활용 추천한다.

Nullable 을 non-Nullable로 변환하는 것이 핵심 => 왜? 내가 사용하기 편하니까

Dto 전체를 변환하는 것이 아니다. 필요한 부분만 변환하는 것이다.
