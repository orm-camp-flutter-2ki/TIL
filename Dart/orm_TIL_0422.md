240422 (Mon)

플러터 과정 30일차


의존성 주입 라이브러리
=

### 기본 의존성 주입
![image](https://github.com/BAUu/TIL/assets/44741680/e74676eb-3d4f-4793-9feb-dd8f95ec02ac)

생성자를 통한 의존성 주입이 기본

### Flutter에서 의존성 주입

- InheritedWidget
- Provider
- Get_it
- GetX
- ...

GetIt 패키지
-
서비스 로케이션 패턴 제공


#### 준비

**Ex) final getIt = GetIt.instance;**

get_it 은 전역으로 사용되는 인스턴스 저장소이다.

top-level 에서 어디서든 쉽게 getIt 으로 접근하도록 위와 같이 준비해서 편하게 쓰기로 함

서비스 로케이터 패턴은 잘못 쓰면 안티 패턴이 된다.

#### 예시

![image](https://github.com/BAUu/TIL/assets/44741680/c7892405-96cd-4e4d-800a-d113130c34f1)

Singleton : 하나의 인스턴스만 존재
Factory : 매번 새로운 인스턴스를 생성

팩토리로 해야 하는 것은 viewModel

나머지는 싱글톤으로 해도 된다.

단 객체 안에서 제공하는 무언가가 있다면 팩토리로 한다.

잘 모르겠다면 팩토리가 안전한 편

### 의존성 조립 코드가 먼저

![image](https://github.com/BAUu/TIL/assets/44741680/abf4ed57-2b03-4a70-ad59-90f503c040a6)

시작 전에 Di 의존성 주입 먼저 설

### Get_It으로 객체를 얻는 경우

```dart
getIt<MainVeiwModel>()
```

getIt<얻을 타입>() 으로 어디에서든 객체를 주입 받을 수 있다.

입력 파라미터 타입에 따라 제네릭은 생략할 수 있다.

## 정리
- 서비스 로케이터 패턴은 잘못 사용하면 완전 안티 패턴임 
- 안전하게 get_it + go_router 셋트로 꼭 go_router 내부에서만 get_it을 사용할 것
- 아무대서나 get_it 을 사용하면 GetX 꼴 난다
- 의존성 조립하는 코드를 잊지말고 꼭 호출한다. test 코드에서도.

#### 참고 자료
[NAVER D2](https://tv.naver.com/v/29723803)

getX 부분을 제외하고 참고
