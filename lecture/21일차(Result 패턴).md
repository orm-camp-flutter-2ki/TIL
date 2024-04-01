# 21일차

## **Result 패턴**

서버에 데이터 요청시 예상되는 상황

- 성공 (Success)
- 실패 (Error, Failure)
    - 네트워크 연결이 아예 안 되어 있음
    - 네트워크 불안정으로 타임아웃 발생
    - 등등

enum은 동등성 및 헤시코드 비교 안되서 한계가 있음 일반적인 클래스 + enum처럼 사용 할 수 있다.

### 에러처리의 기본 try - catch

본적으로 예외는 try - catch 를 활용하여 처리 한다.

런타임 에러 뿐만 아니라 논리적인 오류나 예외 상황에 대한 처리를 하기에는 부족하다

Result 패턴은 성공, 실패시 처리에 유용한 패턴이다

성공과 실패 중 하나를 리턴하는 Result 클래스 예시

- Result 클래스는 성공시에는 데이터를, 실패시에는 Exception(또는 String)을 담는 객체를 정의한다
- 이 외에도 더 많은 반환 케이스가 필요하면 추가하면 된다.
- sealed 클래스는 타입 봉인 효과를 가진다 (enum 하고 비슷한 효과 + 다른 객체의 참조를 가질 수 있다)

```dart
sealed class Result<T> {
 factory Result.success(T data) = Success; // Success 리턴

 factory Result.error(Exception e) = Error;
}

class Success<T> implements Result<T> { // 범용적으로 쓰기 위해서 제네릭 사용
 final T data;

 Success(this.data);
}

class Error<T> implements Result<T> {
 final Exception e;

 Error(this.e);
}

```

```dart
try {
final response = await _client.get(Uri.parse( 
'${Api.baseUr1}?key=keyvalue&q=$query&image_type=photo')); 
Map<String, dynamic> jsonResponse = jsonDecode(response.body); 
Iterable hits = jsonResponse['hits']; 
return hits.map((e) => Photo.fromJson(e)).toList();
return Result.success(hits.map((e) => Photo.fromJson(e)).toList()); 
} catch (e) { |
throw IllegalStateException ('네트워크에러'); 
return const Result.error('네트워크에러');|
}
```

freezed 라이브러리

freezed = json_serializable + Equatable + Immutable 합친 느낌

[https://pub.dev/packages/freezed](https://pub.dev/packages/freezed)

1. toJson / fromJson 함수를 제공해 json으로 쉽게 serialize / deserialize 할 수 있도록 돕는다.

2. equals (==)와 hashCode를 자동으로 작성해준다.

3. 선언된 필드들의 getter를 만들어서 외부에서 값을 변경할 수 없도록 한다.

4. copy와 copyWith을 자동으로 구현해주고, 종속성을 가지는 하위 클래스들에 대해서도 쉽게 deepCopy 할 수 있도록 도와준다.

5. sealed class 작성을 편하게 해 준다

<설치>

dart pub add freezed_annotation

dart pub add dev:build_runner

dart pub add dev:freezed

**// fromJson(), toJson()**

dart pub add json_annotation

dart pub add dev:json_serializable

정리

> 
> 
> - enum 은 클래스만큼 자유롭지 않다
>     - equals, hashcode 재정의가 불가능하다
> - sealed class 는 서브타입을 봉인한다
> - sealed class 는 패턴매칭을 활용하여 모든 서브타입에 대한 처리를 하기 용이하다
> - Result 패턴은 여러가지 종류의 성공과 실패를 처리하기 용이한 패턴이다
> - 앱의 규모에 맞는 Result 패턴을 사용하자
>     - 소규모 ver 1 으로 충분
>     - 다국어 지원 : ver 2

과제1

![Untitled 1](https://github.com/happysong3914/TIL/assets/130008915/ba4af51f-b9e6-412b-a0c4-082f84f50833)


좌측 메뉴중 Collections 에서  New Collection을 선택후 

![Untitled 2](https://github.com/happysong3914/TIL/assets/130008915/5bce0276-564f-44d7-a814-9d3b3a6daad6)


중앙의 화면에서 HTTP request를 선택 (url을 통해서 통신확인)

[https://pixabay.com/api/docs/](https://pixabay.com/api/docs/)

의 설명에서 

[https://pixabay.com/api/docs/](https://pixabay.com/api/docs/)

Retrieving photos of "yellow flowers". The search term q needs to be URL encoded:

![Untitled](https://github.com/happysong3914/TIL/assets/130008915/934b33f6-8286-4cd4-880f-8ad04eaa7973)


해당 내용에서 q에 내용을 바꾸고 정상 통신이되어 결과값 반환을 확인 

q는 검색어 내용임을 확인 검색하고자 하는 내용에 대해서 해당부분의 쿼리스트링 내용에 대해서 값을 달리주어야 하는 것을 확인
