## Model Class의 책임과 역할

* View에 보여질 데이터를 담는 객체
* 비슷한 용어들
  * 도메인 모델
  * Entiity
  * DTO
  * POJO
  * 데이터 클래스(toString, 생성자 등의 6종 세트 포함)

### 모델링 방법
1. DDD(Domain Driven Design)
* Domain의 정의
  * 유사한 업무의 집합
  * 특정 상황(주문, 결재, 로그인)이나 특정 객체(사용자, 손님)가 중심이 될 수 있다.
* 모델 클래스
  * ***도메인을 클래스로 작성한 것!***

2. ORM(Object-relatoinal mapping)
* 데이터 소스가 DB인 경우 DB와 모델 간의 상호 변환을 도와주는 기법


### 모델 클래스 작성 예시
* 일반 클래스
```dart
class User {
  final String name;
  final int age;
  
  User(this.name, this.age);
}
```

* 불변 클래스
  * class 명 앞에 `const` 를 붙인다.
  * const를 붙이면 메모리와 해시 코드가 같아서 메모리를 아낄 수 있다.
  * 컴파일 타임에 불변이 보증되지 않는다면(변수가 들어올 수 있다면), const 사용 안됨

```dart
class User {
  final String name;
  final int age;
  
  const User(this.name, this.age);
}
```

* immutable 어노테이션(flutter에서 사용함)
  * @immutable 어노테이션을 사용하면 불변이 아니면 경고를 표시한다.

* factory 생성자

```dart
class User {
  final String name;
  final int age;
  
  factory User.fromJson(Map<String, dynamic> json) {
    return User(json['name'], json['age']);
  }
}
```

<br></br>

## Model Class의 디자인 패턴
### Factory 패턴
factory(공장)에서 물건을 만드는 것처럼 factory 패턴은 인스턴스를 만드는 패턴

<img width="300" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/6458f4b7-8a17-4f31-928d-8d213a62e2f4">
(어떤 형태의 인스턴스를 줄 것인지를 만든다.)

### Singleton 패턴
1개의 인스턴스만 생성되는 것을 보증하기 위한 패턴

<img width="300" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/cffd99be-939b-415f-b57c-e633b3ab82a6">

* 여러개의 인스턴스를 생성해도 1개의 인스턴스가 공유된다.(렌터카 같은 개념)
* 공유 자원처럼 사용된다.
* 캐시나 공유 데이터, 처리의 효율화 등에 사용된다.

<img width="303" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/c9c22b00-0ec5-4d9f-88ad-aab2eccedddf">

기본 생성자(User user = User();)는 따로 재정의가 안돼있어야지 사용할 수 있다.  
<img width="200" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/33230f08-ae04-40b6-9abd-81c236dd864e">
그래서 singleton 생성자를 만들면 기본 생성자 호출을 못 한다. 

<img width="350" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/57022299-dc10-4a11-93fc-adec6a58ce32">
static 인스턴스를 만들고 named construntor를 담아준다.

factory 생성자에서 그 인스턴스를 리턴해준다.
<img width="200" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/9b68d759-dbfb-4c2f-b993-65e1f3ec08b8">

=> 그러면 const를 붙이지 않아도 그 클래스로 만든 값의 메모리는 동일하다.

<br></br>

* 앞서의 예시처럼 모델 클래스를 만드는 방법은 여러가지가 있다.
* 프로젝트 성격에 따라 다양한 방식으로 모델 클래스를 정의할 수 있다.

<br></br>

## Repository 패턴
* 데이터 저장소에 접근하는 객체를 추상화하고
* 데이터 소스(DB, File 등)와의 통신을 담당하는 객체를 캡슐화하는 디자인 패턴

<img width="358" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/8e5bd411-90e5-40a8-84f7-73c021c42a43">

* 데이터 소스에서는 데이터만 가져오고
* 앱에 필요한 로직을 생성하여 레포지토리에 정의
   => 수정이 필요할 때, 레포지토리만 수정하면 된다.

### Repository의 책임과 역할
* 데이터 소스와 상호 작용하여 데이터를 추가, 조회, 수정, 삭제(CRUD)하는 역할을 담당
* ✅ **데이터 캡슐화**
* ✅ **데이터 추상화**
* 데이터 접근 제어
* 예외 처리

* 장점
  * 유지 관리서 향상
  * 재사용성 향상
  * 테스트 용이성 향상
  * 확장성 향상
  * ✅ **데이터 액세스 추상화**

### 소규모 프로그램에서 DB를 조작(CRUD)하는 Repository 클래스 예시
<img width="403" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/8c2f1959-7444-4cf0-8b87-2083c2966386">

#### 확장을 고려한 Repository 패턴 작성 예시
* 데이터 추상화를 위한 인터페이스를 정의
```dart
abstract interface class AlbumRepository {
  Future<List<Album>> getAlbums();
  Future<List<Album>> getAlbumsTop10();
}
```

* 구현체 작성
```dart
class AlbumRepositoryImpl implements AlbumRepository {
  AlbumApi albumApi = AlbumApi();

  @override
  Future<List<Album>> getAlbums() async {
    return await albumApi.getAlbums();
  }

  @override
  Future<List<Album>> getAlbumsTop10() async {
    final getData = await albumApi.getAlbums();
    return getData.sublist(0, 10);
  }

}
```

* 인터페이스를 활용했을 때의 장점
  * 객체 지향 프로그래밍의 다향성을 잘 활용한 예
  * 테스스 용이

<br></br>

## 기타
* DeepCollectionEquality().equals(actualData, expectedData)를 사용하면 해시코드가 달라도 Map 컬렉션 내부의 내용 비교가 가능하다.
* 기본 값(int, double, String)들은 불변이기 때문에 같은 값이 들어간다면 모두 재사용된다.
```dart
// identical : 메모리 주소 비교
final user1 = User('name', 10);
final user2 = User('name', 10);

print(identical(user1, user2)); // 동일
```
